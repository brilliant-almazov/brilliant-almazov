# Platform architecture

High-level picture of the microservice platform I designed and ship in production. Names of internal services are abstracted; the patterns are not.

## The product

A marketing & SEO analytics platform for the gaming vertical:

- Crawls and re-crawls millions of pages, keywords, competitors.
- Classifies, scores, deduplicates and stores the results.
- Serves the data to internal dashboards and external marketing partners over gRPC.
- Runs scheduled analytical jobs in BigQuery against the warehouse.

## Why we're rebuilding

We started on a large PHP / Symfony monolith. It works, but it's expensive:

- Per-worker memory footprint of 100+ MB (a typical Symfony daemon sits around ~150 MB).
- Framework overhead of 50–200 ms on every metrics scrape.
- Long-running background jobs sharing the same Symfony bootstrap as HTTP handlers.
- Hard to scale individual hot paths independently.

The plan: leave PHP doing what it's good at (the admin / business UX), peel off the hot and async parts into Go services, instrument everything from day one, and don't touch any of it without metrics.

## Topology

```
                           ┌──────────────────────┐   ┌──────────────────────┐
                           │  Admin UI            │   │  External partners   │
                           │  React + Mantine     │   │  (gRPC clients)      │
                           └──────────┬───────────┘   └──────────┬───────────┘
                                      │                          │
                                      ▼                          ▼
                           ┌──────────────────────┐   ┌──────────────────────┐
                           │  Admin BFF (Go)      │   │   Gateway (Go)       │
                           └──────────┬───────────┘   └──────────┬───────────┘
                                      │                          │
                                      │            ┌─────────────┼────────────┬──────────────┐
                                      │            │             │            │              │
                                      ▼            ▼             ▼            ▼              ▼
                  ┌────────────────────────────────────────────────────────────────────────────────────┐
                  │                          Go microservices (growing)                               │
                  │ Content scraper · Domain-rule map · Dictionary replica · AI assistant · Gateway   │
                  └────────────────────────────────────────────────────────────────────────────────────┘
                                      ▲   ▲           │   │           │
                                      │   │           │   │           │
                                      │   │   gRPC    │   │   NATS    │   pgx
              ┌───────────────────────┘   │           │   ▼           ▼
              │                           │     ┌────────────┐  ┌───────────────┐
   ┌──────────┴─────────────┐             │     │   NATS     │  │  PostgreSQL   │
   │ PHP / Symfony monolith │ ◀─── gRPC ──┘     │ JetStream  │  └───────────────┘
   │      (shrinking)       │                   └──────┬─────┘
   │  • HTTP API            │                          │
   │  • Background workers  │ ◀────── subscribe ───────┘
   └──────────┬─────────────┘
              │
              ├─────────────▶  Redis  (cache, rate-limit, PHP metrics store)
              ├─────────────▶  RabbitMQ  (legacy bus — being drained)
              └─────────────▶  BigQuery  (analytics warehouse, DAGs)

   ┌───────────────────────────────────────────────────────────────────────────────┐
   │                          Platform — owned by me                              │
   │                                                                              │
   │   ┌─────────────┐    register / proxy    ┌──────────────────────────────┐    │
   │   │  Registry   │  ◀───── Ed25519 ─────  │  Sidecar (Rust, ~3 MB)       │    │
   │   │  (Go,       │   ───── heartbeat ──▶  │  manages PHP & Go processes  │    │
   │   │   single    │                        │  drop-in supervisord replace │    │
   │   │   writer)   │                        └──────────────────────────────┘    │
   │   └─────────────┘                                                            │
   │                                                                              │
   │   Platform library (Go) — imported by every Go service:                      │
   │     resource lifecycle · gRPC / HTTP / Postgres / NATS / RabbitMQ wrappers   │
   │     outbox · Snowflake IDs · structured logging · Prometheus metrics         │
   │     testcontainers-go harness · goose migrations · zero defaults             │
   └───────────────────────────────────────────────────────────────────────────────┘
```

## Layers

### 1. Sidecar (Rust)

A static ~3 MB binary that replaces supervisord inside PHP containers.

- Reads existing supervisord configs without modification — zero PHP deploy changes.
- Manages process lifecycle (start, stop, restart, scale).
- Exposes a small HTTP API for control and `/metrics` for Prometheus.
- Registers with the registry on startup (mutual Ed25519 auth).
- Sends signed heartbeats; registry can also pull `/healthz` for two-sided liveness.

**Why Rust:** no GC, predictable memory, small static binary, async via `tokio`, easy to embed in any PHP image as a single file.

**What it replaced:** a ~50 MB Python supervisord runtime per container.

### 2. Registry (Go)

The control plane. The single writer for "who is alive, where, and in what shape".

- `POST /api/v1/register` from sidecars on start.
- Signed `POST /api/v1/heartbeat` + active pull of `/healthz`.
- `GET /api/v1/services[/{id}/replicas[/{id}]]` for the admin UI.
- Reverse proxy: `/api/v1/services/{id}/replicas/{id}/processes/*` and `/scale` forwarded to the right sidecar with Ed25519 signing by the registry.

**Why this exists:** in a multi-replica world, talking to one supervisord per container doesn't scale. Operators talk to the registry; the registry talks to sidecars.

### 3. Platform library (Go)

Imported by every Go service. Defines the one way to do everything.

- **Resource lifecycle:** `App.UseResource(name, factory)` — gRPC, HTTP, Postgres, NATS, RabbitMQ, Redis, etc. Each resource is a struct with `Start` / `Stop`, registered through a DI provider chain (no fx).
- **Handlers:** `platform.GRPCHandler`, `platform.HTTPHandler`. Service code implements them; the platform wires routing, middleware, metrics, recovery.
- **Outbox:** Postgres-backed event outbox with NATS publisher. At-least-once delivery, exactly-once business logic via idempotency keys.
- **Messaging:** generic NATS / RabbitMQ consumers with retries, dead-letter handling, structured ack/nack.
- **Observability:** every driver and client publishes Prometheus metrics per operation. Structured zap logs with trace context.
- **Snowflake IDs:** every entity uses Snowflake `BIGINT` IDs — no `SERIAL`, no `UUID` on the hot path.
- **Migrations:** `pressly/goose/v3` with `embed.FS`. A post-step rewrites the `goose_db_version` table to add a `name` column derived from the filename — far easier to read than goose's default `tstamp`.
- **Test harness:** `testcontainers-go` with one Postgres / NATS / RabbitMQ per test run, namespace-isolated data per test, explicit teardown.

### 4. Service template

Scaffold for new Go services. Replaces "let's create a microservice" — a half-day exercise — with "rename a directory and edit two configs".

Every service that comes out of the template is:

- gRPC-first.
- Wired into NATS via the outbox.
- Migrated by goose.
- Exposing `/metrics`, `/healthz`, `/readyz` on a separate system port.
- CI-ready: tests, lint, coverage gate, binary build, Docker image, version badge.

## How services talk to each other

```
   PHP monolith       Gateway (Go)      Content (Go)      PostgreSQL       NATS         Worker (Go)
        │                  │                  │                │              │                │
        │ gRPC SubmitTask  │                  │                │              │                │
        │ ────────────────▶│                  │                │              │                │
        │                  │ gRPC SubmitTask  │                │              │                │
        │                  │ ────────────────▶│                │              │                │
        │                  │                  │ INSERT task    │              │                │
        │                  │                  │ + N entities   │              │                │
        │                  │                  │ ──────────────▶│              │                │
        │                  │                  │ INSERT outbox  │              │                │
        │                  │                  │ event          │              │                │
        │                  │                  │ ──────────────▶│              │                │
        │                  │                  │   (same SQL transaction)      │                │
        │                  │  ack             │                │              │                │
        │ ◀────────────────────────────────── │                │              │                │
        │                  │                  │                │              │                │
        │                  │                  │                │              │ SELECT outbox  │
        │                  │                  │                │              │ status=pending │
        │                  │                  │                │ ◀───────────────────────────  │
        │                  │                  │                │              │ publish        │
        │                  │                  │                │              │ scrape.request │
        │                  │                  │                │              │ ◀──────────────│
        │                  │                  │                │              │                │
        │                  │                  │                │              │ scrape.delivered (from provider)
        │                  │                  │                │              │ ──────────────▶│
        │                  │                  │                │              │ UPDATE entity  │
        │                  │                  │                │              │ state          │
        │                  │                  │                │ ◀──────────────────────────── │
```

Every event that leaves a service goes through Postgres outbox first. The publisher is a background loop inside the worker, drained by NATS. This gives us at-least-once delivery without distributed transactions — the database row and the event live in the same SQL transaction.

## What I optimise for

- **Boring, predictable, observable.** A new on-call engineer should be able to read `/metrics` and Grafana and understand the state of any service in five minutes.
- **One way to do things.** If two services do the same thing differently, one of them is wrong, and it usually means the platform library is missing a feature.
- **Backpressure over retries.** When something downstream is slow, we slow down the producer through NATS consumer pull limits, not by retrying harder.
- **Static binaries everywhere.** Rust sidecar and Go services build to single static binaries running on `alpine` images. Final container size measured in tens of MB.
- **No surprise behaviour in shared code.** Shared libraries have zero defaults. The caller passes config explicitly. If the caller forgets, the service fails to start, not in production three weeks later.

## What's next

- Tracing (OpenTelemetry) baked into the platform library.
- A small Go scheduler for cron-style background jobs, replacing the last PHP cron container.
- Internal feature flags (a small wrapper over a Postgres-backed flag table).
- A gRPC-to-public-REST gateway for partner-facing APIs (we currently expose gRPC + a thin Go HTTP shim).
