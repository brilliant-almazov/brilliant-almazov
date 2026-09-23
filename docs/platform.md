# Platform abstractions

> **Goal:** ship a new microservice in a day, not a sprint — wired into observability,
> messaging, persistence and process supervision from the first commit.

In most companies, starting a service means picking frameworks, copying `main.go` from a
sibling, wiring metrics, fighting migration tooling, writing a Dockerfile and configuring the
observability stack. Here it means: clone the template, rename two configs, write the handler.

---

## 1. A Go platform library, imported by every service

The library defines **one way** to do everything that is not domain logic.

- **Resource lifecycle.** A single `UseResource(name, factory)` API for every resource kind:
  gRPC server, HTTP server, Postgres pool, bus client, cache client. Each resource is a struct
  with `Start` / `Stop`, registered through an explicit provider chain — no magic container.
  Start order is deterministic, shutdown is graceful and ordered.
- **Transport handlers.** Service code implements a handler interface; the platform wires
  routing, middleware, metrics, recovery, trace context and request IDs.
- **Outbox.** A Postgres-backed event outbox with a bus publisher. The event row is written in
  the same SQL transaction as the business write; a background loop drains it. At-least-once
  delivery, idempotent consumers, no distributed transactions.
- **Generic workers.** One pipeline — `source → preparer → reader → coalescer → consumer →
  processor → status update` — with pluggable patterns (migrator, outbox, CDC, consumer,
  scheduler, delayed). Only the reader and the processor differ between them.
- **Typed consumers.** `Listen[T proto.Message]` with retries, dead-letter handling and
  structured ack / nack.
- **Snowflake IDs** for every entity: sortable, shard-friendly, no sequence contention.
- **Migrations.** An embedded-filesystem runner, forward-only, with readable version names.
- **Observability primitives.** Per-operation counters and histograms in every driver,
  structured logs carrying trace context, health and readiness on a separate system port.
- **Test harness.** Integration tests on real infrastructure through testcontainers: one
  container set per test run, namespace isolation per test, explicit teardown. Never mocks for
  infrastructure.

## 2. A service template

A scaffold repository that clones into a working service: transport wiring, server and worker
entry points, embedded migrations, metrics and health endpoints on a system port, a multi-stage
Dockerfile producing a 20–30 MB image, and a CI pipeline with tests, lint, a coverage gate,
binary and image build.

> The first commit in a new service is the contract and the handler. The rest already exists.

## 3. A Rust sidecar instead of a general-purpose supervisor

A ~3 MB static binary that supervises processes inside a container: lifecycle (start, stop,
restart, scale), a small control API, a Prometheus endpoint, and registration with the control
plane over mutually authenticated Ed25519 signatures. It reads the previous supervisor's config
format unchanged, so adoption costs no deploy changes. It replaced a ~50 MB Python-based
runtime — roughly a 17× reduction in process-manager footprint.

**Why Rust:** no GC, predictable memory, a single static binary that drops into any image.

## 4. A control-plane registry

The single writer for *who is alive, where, and in what shape*: registration from sidecars,
signed heartbeats plus health pulls from the registry side, a read API for operational UIs, and
a signed reverse proxy for process control and scaling.

## 5. Contracts as artefacts

Protocol Buffers live in their own repository and generate stubs for every language in the
estate. Contract changes are reviewed as changes to an artefact, not as a side effect of code.

---

## What the platform refuses to do

- No defaults in shared libraries: a missing setting fails the boot, not production later.
- No per-service reinvention of retries, metrics, migrations or bus plumbing.
- No infrastructure mocks in tests that claim to cover infrastructure.
