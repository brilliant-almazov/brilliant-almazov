# Platform abstractions

> **Goal:** ship a new microservice in a day, not a sprint. Wire it into observability, messaging, persistence and process supervision from the first commit.

The platform is the answer to the question: *"What does it take to start a new microservice?"* In most companies the answer is "a sprint" — pick frameworks, copy `main.go` from a sibling, wire metrics, set up CI, fight the migration tooling, set up testcontainers, write the Dockerfile, configure the observability stack. In this platform the answer is **clone the template, rename two configs, write the handler.** Everything else is already there.

---

## What the platform gives you

### 1. A Go platform library — imported by every service

The library defines **one way** to do everything that is not domain logic. It owns:

- **Resource lifecycle.** A single `App.UseResource(name, factory)` API for every kind of resource: gRPC server, HTTP server, Postgres pool, NATS client, RabbitMQ client, Redis client. Each resource is a struct with `Start` / `Stop`, registered through a DI-style provider chain (no `fx`, no magic). Start order is deterministic; shutdown is graceful and ordered.
- **Transport handlers.** `platform.GRPCHandler`, `platform.HTTPHandler` interfaces. Service code implements them — the platform wires routing, middleware, metrics, recovery, tracing context, structured request IDs.
- **Outbox pattern.** A Postgres-backed event outbox with a NATS publisher. Domain events are written to the outbox row **in the same SQL transaction** as the business write. A background loop drains the outbox into NATS. At-least-once delivery, no distributed transactions, idempotent consumers handle replay.
- **Generic workers.** A `worker` abstraction with six pluggable patterns (Migrator, Outbox, CDC, Consumer, Scheduler, Delayed) all sharing the same pipeline: `source → preparer → reader → coalescer → consumer → processor → status update`. Difference between patterns is only the *reader* and the *processor*.
- **Generic NATS / RabbitMQ consumers.** Strongly-typed (`Listen[T proto.Message]`) with retries, dead-letter handling, structured ack/nack.
- **Snowflake IDs.** Every entity uses Snowflake `BIGINT` IDs — never `SERIAL`, never `UUID` on the hot path.
- **Migrations.** `pressly/goose/v3` + `embed.FS` runner. A post-step rewrites `goose_db_version` to add a `name` column derived from the filename — far easier to read than goose's default `tstamp`.
- **Observability primitives.** Every driver and client publishes Prometheus counters and histograms per operation. Structured zap logs carry trace context. Health / readiness endpoints are mounted on a separate system port automatically.
- **Test harness.** `testcontainers-go` integration tests with **one** Postgres / NATS / RabbitMQ container per `go test` run, namespace-isolated data per test, explicit teardown via `trap EXIT`. No mocks for infrastructure.

### 2. A service template

A scaffold repo. Cloning it gives you a working service:

- gRPC-first wiring.
- `cmd/server` + `cmd/worker` split if needed.
- Goose migrations with `embed.FS`.
- `/metrics`, `/healthz`, `/readyz` on a separate system port.
- Dockerfile (multi-stage, ~20–30 MB final image on `alpine`).
- GitHub Actions: tests, lint, coverage gate, binary build, image build, image push, version badge.
- Linked into the org-wide observability (Grafana folder, Prometheus scrape config).

> The first commit in a new service is your `proto` file and your handler. Everything else is already done.

### 3. A Rust sidecar (replaces supervisord)

A **~3 MB static musl binary** that manages PHP and Go processes inside any container.

- Reads existing supervisord configs **without modification** — drop-in replacement, zero PHP deploy changes.
- Process lifecycle: start, stop, restart, scale.
- Small HTTP API for control + `/metrics` for Prometheus.
- Registers with the control-plane registry on startup (mutual Ed25519 auth).
- Sends signed heartbeats; the registry also pulls `/healthz` for two-sided liveness.

**Why Rust:** no GC, predictable memory, small static binary, async via `tokio`, easy to embed in any PHP image as a single file.

**What it replaced:** a ~50 MB Python supervisord runtime per container. About **17× reduction** in process-manager footprint.

### 4. A Go control-plane registry

The single writer for *"who is alive, where, in what shape"*.

- `POST /api/v1/register` from sidecars on start.
- Signed `POST /api/v1/heartbeat` + active pull of `/healthz` from registry side.
- `GET /api/v1/services[/{id}/replicas[/{id}]]` for admin UIs.
- Reverse proxy: `* /api/v1/services/{id}/replicas/{id}/processes/*` and `/scale` forwarded to the right sidecar with Ed25519 signing by the registry.

**Why this exists:** in a multi-replica world, talking to one supervisord per container doesn't scale. Operators talk to the registry; the registry talks to sidecars.

### 5. A shared schema repo (Protocol Buffers)

One repo for all gRPC schemas, generated stubs for Go and PHP. **No raw HTTP between internal services.** Versioned, with buf-style discipline.

---

## What you don't think about (because the platform did)

- "How do I expose `/metrics`?" — already done.
- "Where do my structured logs go?" — `zap`, JSON, trace-context-aware.
- "How do I do at-least-once messaging?" — outbox + NATS, already wired.
- "How do I migrate the database?" — goose, embedded, forward-only, with linting.
- "What's the test infrastructure?" — testcontainers, one container per run, namespace-isolated.
- "How do I get an ID?" — Snowflake helper.
- "How do I handle a typed NATS message?" — `Listen[T proto.Message]`.
- "How do I read config?" — single typed `Config` struct per service. No defaults in shared libs.
- "How do I report `/healthz` + `/readyz`?" — automatic, on system port.
- "How do I sign / verify a sidecar request?" — Ed25519 helper.
- "How do I build a Dockerfile?" — multi-stage, in the template.
- "How do I get a coverage badge?" — CI publishes it.

---

## Why this matters

A new service costs almost nothing to start. That's the unlock that makes a polyrepo distributed system actually viable: when adding a new service is a half-day exercise, **bounded contexts can be small and many**, not "one giant service per team because spinning up a new one is too painful."

It also means the migration off the PHP monolith is **strangler-friendly**: every new bounded context becomes its own service the moment its responsibilities are clear, instead of waiting for a "big rewrite milestone" that never ships.

---

## What's next

- **OpenTelemetry tracing** baked into the platform library — tracers wired into every transport driver automatically.
- **Internal feature flags** — small Postgres-backed flag wrapper, with a CLI and admin UI.
- **A Go cron scheduler** to replace the last PHP cron container.
- **gRPC-to-public-REST gateway** for partner-facing APIs (currently exposed via a thin Go HTTP shim).
- **Per-package `worker` convenience wrappers**: `worker.NewMigrator`, `worker.NewOutbox`, `worker.NewConsumer`, `worker.NewScheduler`, `worker.NewDelayed`, and richer consumer flavours (chunked / parallel / grouped / throttled).
