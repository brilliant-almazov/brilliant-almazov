# Platform architecture

The architecture of the microservice platform I design and operate. Product, domains and
internal service names are deliberately out of scope — the patterns are the point.

## Starting position

A well-structured Symfony monolith: clean, domain-driven, actively maintained. It is being
replaced service by service for resource efficiency and independent scaling, not because the
code is bad. The costs that drive the move are structural:

- 100+ MB of framework bootstrap per worker process (a typical daemon sits around ~150 MB).
- 50–200 ms of framework overhead on hot paths such as a metrics scrape.
- Background jobs sharing the same bootstrap as HTTP handlers, so neither scales alone.

## Topology

```
   ┌──────────────┐        ┌──────────────────┐
   │  Admin UI    │        │  External gRPC   │
   └──────┬───────┘        └────────┬─────────┘
          │                         │
          ▼                         ▼
   ┌──────────────┐        ┌──────────────────┐
   │  Admin BFF   │        │     Gateway      │
   └──────┬───────┘        └────────┬─────────┘
          │                         │
          ▼                         ▼
   ┌────────────────────────────────────────────┐
   │          Go services (one per context)     │
   │  gRPC server · worker · outbox · scheduler │
   └───────┬───────────────┬────────────┬───────┘
           │ gRPC          │ bus        │ pgx
           ▼               ▼            ▼
   ┌──────────────┐  ┌───────────┐  ┌────────────┐
   │   Monolith   │  │  NATS     │  │ PostgreSQL │
   │  (shrinking) │  │ JetStream │  │ per service│
   └──────────────┘  └───────────┘  └────────────┘
```

## Rules that hold everywhere

**A service owns its database.** No shared schema, no cross-service SQL. Data crosses a
boundary as a contract call or as an event, never as a join.

**Writes leave through a transactional outbox.** The domain write and the event row land in
one SQL transaction; a drain loop publishes to the bus. At-least-once delivery, idempotent
consumers, no distributed transactions.

**Contracts are artefacts.** Protocol Buffers live in a shared repository and generate stubs
for every language in the estate. The schema changes before the code does.

**Synchronous where an answer is required, asynchronous everywhere else.** gRPC for request
and response, the bus for propagation and fan-out.

**Every binary is twelve-factor.** Configuration arrives through the environment, there are no
defaults in shared libraries, and a missing value fails the boot rather than production.

**Observability is not optional wiring.** Every driver publishes counters and histograms per
operation, logs carry trace context, health and readiness live on a separate system port.

## Service shape

One context ships as several binaries from one repository: a gRPC server, a worker, an outbox
drainer, a scheduler. They share the domain package and the platform library, and they scale
independently.

## What this buys

| Measured | Before | After |
|---|---|---|
| Memory per worker | ~150 MB | ~20 MB, ~7× |
| Container image | 100+ MB | 20–30 MB, 5–10× |
| Metrics scrape | 50–200 ms | sub-millisecond |
| New service to production | ~1 week | 1 day |

See also [platform.md](./platform.md) for the library and the template,
[migration.md](./migration.md) for the method of peeling a context off a monolith.
