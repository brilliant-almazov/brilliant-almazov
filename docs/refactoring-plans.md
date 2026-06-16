# Active refactoring plans

> Refactoring is a continuous process here, not a "milestone-13 epic". These are the active plans currently in flight — each backed by Linear tickets, design docs, and a strangler-style execution plan.

This document captures the *direction*, not the per-ticket detail. Internal repo names and ticket IDs are intentionally omitted.

---

## 1. Admin → strangler split: monolith → 5 services + UI

### Where we are

The admin & operational control plane is currently a single Go binary serving six domains (`auth`, `database`, `config`, `audit`, `reports`, `decode`) plus a standalone `migrator` binary. The UI is one React SPA bundling everything.

It works. It also has the pain that every monolith eventually has:

- Heavy deploys — any change drags the whole build.
- No independent evolution of domains — a tiny change to `audit` ships with the world.
- Hard to test in isolation — touching one domain risks regressions in another.
- UI deploys take 5 minutes for what should be a 30-second static-asset push.

### Where we're going

Five backend services + one (later: multiple) UI bundle:

```
                              ┌──────────────────┐
                              │   UI bundle      │
                              │   (static + SSE) │
                              └────────┬─────────┘
                                       │ HTTPS / SSE
                                       ▼
                              ┌──────────────────┐
                              │  Gateway         │  public endpoint
                              │  REST + SSE in   │  auth (Zitadel)
                              │  gRPC out        │  CORS · rate limit
                              └─┬──┬──┬──┬──┬───┘  session · telemetry
                                │  │  │  │  │
                                ▼  ▼  ▼  ▼  ▼     gRPC (internal)
                          ┌────────────────────────────────────────┐
                          │  core-svc · data-svc · ops-svc ·       │
                          │  github-svc · (more later)             │
                          └────────────────────────────────────────┘
                                       │
                                       ▼
                          PostgreSQL · Redis · NATS · S3 · GitHub API
```

| Service | Owns |
|---|---|
| **gateway** | Public surface. REST + SSE in, gRPC out. Auth, sessions, CORS, rate-limit, telemetry, SSE fan-in. |
| **core-svc** | Auth / session / users / configs / preferences / dictionaries / enums / audit / reports / dashboards. |
| **data-svc** | Data sources, schemas, tables, queries, matviews, partitions, functions, server processes. |
| **ops-svc** | Migrator, archive, smart copy, scheduled jobs. (Subsumes the standalone migrator binary.) |
| **github-svc** | GitHub aggregator — repos, PRs, CI status, commits, releases. Cached via Redis, invalidated via webhooks. |
| **ui** | Currently one SPA. Eventually splits into micro-frontends matching the backend boundaries. |

### Phasing (strangler)

| Phase | What | Win |
|---|---|---|
| **0 — Foundation** | Stand up the shared schema repo, the gateway shell, the GitHub-aggregator service repo, and the standalone UI repo. Add tracing (OTLP collector). Update local docker-compose to host all 5 services. | UI deploy decoupled — 30 s instead of 5 min for UI-only changes. No user-visible change. |
| **1 — First microservice (github-svc)** | Build the first end-to-end service: proto contract, Redis-cached GitHub client, gRPC server, SSE through gateway, webhook receiver, new UI page. | Pattern proved on an isolated domain. PR / CI visibility unified. |
| **2 — ops-svc** | Wrap the existing standalone migrator + archive jobs in a gRPC server. Gateway proxies `/api/migrator/*`. | Standalone binary disappears; operations are first-class. |
| **3 — data-svc** | Move data-source / schema / tables / queries logic out of the monolith into its own service. | Read-heavy domain isolated; admin monolith shrinks by ~30 %. |
| **4 — core-svc** | The last and largest peel-off. Auth / session / configs / preferences / audit / reports. By this point the monolith is mostly hollow — what remains becomes core-svc. | Monolith dies. |
| **5 — Micro-frontends** | Once backends are stable, split the SPA into per-domain bundles. | Independent UI deploys per domain. |

Each phase ships behind the gateway. The monolith stays alive throughout, gradually losing responsibilities. **No flag day. No big-bang rewrite.** Risk is contained per phase.

### Costs we accept

- A shared `proto` repo with buf-style discipline (already exists for the platform side; reused here).
- Tracing (OTel) to make multi-service debugging tolerable.
- Five-service local docker-compose for dev — heavier, but each service stays small.
- Gateway-side auth — Zitadel session validation, RBAC enforcement, SSE fan-in.

These are *real* costs. They buy independent evolution of domains, independent deploy, independent scaling, smaller blast radius — for what is now the most operationally-critical surface of the platform.

---

## 2. Platform worker abstraction: 6 patterns, 1 pipeline

### Where we are

Across the existing PHP / Symfony monolith, six distinct worker patterns live, hand-coded in slightly different shapes:

| Pattern | What it does |
|---|---|
| **Migrator** | One-time / on-startup data migration runners. |
| **Outbox** | Background drain of a Postgres outbox table into a message bus. |
| **CDC** | Change-data-capture — react to row state changes. |
| **Consumer** | Subscribe to a message bus, process messages, ack / nack. |
| **Scheduler** | Cron-like periodic tasks. |
| **Delayed** | Schedule work to run at / after a specific time. |

Each implementation is its own snowflake — different retry policy, different observability, different config surface. Migrating any of them to Go currently means re-deriving the framework from scratch.

### Where we're going

A single platform-level **worker abstraction**. All six patterns share the same pipeline:

```
source  →  preparer  →  reader  →  coalescer  →  consumer  →  processor  →  status update
```

The **only** differences between patterns are:

- **Reader** — where messages come from (Postgres table, NATS subject, RabbitMQ queue, Redis stream, in-memory cron tick).
- **Processor** — what is done with each message (HTTP call, gRPC, business handler, …).

Everything else — concurrency control, retries, dead-lettering, status transitions, metrics, structured logging, admin gRPC for enable / disable / concurrency — is shared.

### Phasing

| Phase | What |
|---|---|
| **1 — Core (in progress)** | Core interfaces + table source + Init phase + minimal coalescer / consumer + NATS broker source + publisher + two reference examples. |
| **2 — Admin API & convenience wrappers** | Admin gRPC (enable / disable / change concurrency). Per-pattern factory helpers (`worker.NewMigrator`, `worker.NewOutbox`, `worker.NewConsumer`, `worker.NewScheduler`, `worker.NewDelayed`). |
| **3 — Richer readers / consumers** | RabbitMQ pull-reader, Redis stream reader, priority reader. Chunked / parallel / grouped / throttled consumer flavours. |

### Why this matters

The PHP monolith has dozens of worker-shaped processes. Most are simple "poll table → process → publish". With the worker abstraction, **migrating any one of them to Go is a one-day exercise**: write a reader, write a processor, register, deploy. Everything else — observability, lifecycle, admin control, error handling — is given.

This is the lever that turns "PHP → Go migration" from a multi-quarter project into a steady, predictable flow.

### Standard contracts

A worker pulling from a Postgres table sees this contract:

```sql
CREATE TYPE worker_status AS ENUM ('pending', 'done', 'failed');

CREATE TABLE example_queue (
    id            BIGINT        PRIMARY KEY,  -- snowflake
    status        worker_status NOT NULL DEFAULT 'pending',
    error_message VARCHAR       NULL,
    created_at    TIMESTAMP(6)  NOT NULL DEFAULT NOW(),
    updated_at    TIMESTAMP(6)  NULL,
    payload       JSONB         NOT NULL
);
```

Enum values are a recommendation; concrete services pick their own state machine (`pending → published`, `pending → in_progress → finished`, etc.). The abstraction is shape-agnostic — it cares about *transitions*, not *names*.

---

## 3. Smaller plans currently in flight

- **OpenTelemetry tracing baked into the platform library.** Tracers wired into every transport driver automatically — gRPC / HTTP / NATS / RabbitMQ / Postgres.
- **Internal feature flags.** Small Postgres-backed flag wrapper with a CLI and an admin UI.
- **Go cron scheduler** to replace the last PHP cron container.
- **gRPC-to-public-REST gateway** for partner-facing APIs (currently exposed via a thin Go HTTP shim).
- **External public IdP for the partner-facing API.** Currently authenticated by an internal-only contract; moving toward Zitadel-as-IdP for partners as well.
- **PHP-sender legacy demolition.** Progressive removal of Go code that exists only to talk to PHP-side senders. PHP itself is left alone for now — we tear the Go-side scaffolding down as services migrate over.

---

## How plans become work

Every plan above is decomposed into Linear tickets with estimates (1 pt ≈ 1 h of Claude execution). Each ticket carries its budget tracking (time, tokens, money, ops) and incident log (Claude mistakes, scope changes, spec ambiguity, tech surprises). The patterns where the AI drifts feed back into stricter `CLAUDE.md` rules and tighter hooks — see [`ai-engineering.md`](./ai-engineering.md) for the loop.
