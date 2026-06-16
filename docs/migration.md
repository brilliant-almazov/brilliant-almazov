# PHP → Go migration

> **The legacy is a multi-million-LOC PHP / Symfony monolith.** It works. It's also expensive. We're peeling it apart, service by service, into Go microservices on top of the [platform](./platform.md).

This is not a "rewrite the world" project. It's a **strangler migration with metrics at every step**.

---

## Why we're doing this

The PHP monolith is the historical core of the product. Symfony, MySQL, RabbitMQ, Consul. It carries 15 years of accumulated domain logic. Three things make it expensive at the current scale:

1. **Per-worker memory.** 100+ MB of Symfony bootstrap per worker process — a typical PHP daemon sits around ~150 MB resident. Multiply by N workers per machine and the bill adds up quickly.
2. **Framework overhead on hot paths.** A simple `/metrics` scrape goes through 50–200 ms of Symfony bootstrap. Internal request latency suffers the same way.
3. **No independent scaling.** Background jobs share the same Symfony bootstrap as HTTP handlers. You can't scale one without paying for the other.

The PHP monolith is good at what it's good at — the rich admin / business UX, deeply Symfony-flavoured domain models, decades of polish. **We're not throwing it away.** We're moving the hot, async and infrastructure-bound parts to Go, and leaving the parts where Symfony still wins.

---

## What we measure

| Layer | Before (PHP) | After (Go / Rust) | Improvement |
|---|---|---|---|
| Per-worker resident memory | 100+ MB (typical Symfony daemon ~150 MB) | **~20 MB per Go binary** | **~7×** |
| Container image size | 100+ MB (PHP/Symfony image) | **~20–30 MB final (Go on alpine)** | **5–10×** |
| Process-manager footprint | ~50 MB Python supervisord | **~3 MB Rust sidecar** | **~17×** |
| Prometheus scrape latency (PHP-Redis metrics) | 50–200 ms via Symfony | **sub-millisecond via Rust bridge** | **50–200×** |
| BigQuery cloud bill (data-layer redesign) | baseline | **up to 10× reduction** | **10×** |
| Client launch workflow | 1–2 hours | **15 minutes** | **4–8×** |

These are not synthetic benchmarks. They are differences observed on the same production workload, before and after each peel-off.

---

## How we peel a service off

For every bounded context being extracted from the PHP monolith, the pattern is:

1. **Define the bounded context.** What data does this own? What writes? What reads?
2. **Lock down the contract.** Add a gRPC schema to the shared proto repo. The PHP side gets a generated client; the Go side gets a generated server.
3. **Run dual-write or async replication.** Either PHP writes to both old + new (dual-write), or the Go service is an async replica drained via an outbox + NATS (cleaner for read-heavy domains).
4. **Switch readers over.** PHP read paths swap from the local DB to the gRPC client.
5. **Drop the PHP-side write path.** Once readers are stable on the new service and back-pressure is verified.
6. **Reclaim resources.** Old PHP workers, daemons, schemas go.

Each step is measurable in Grafana — we don't move on until the metrics show the new path is healthy.

---

## What's already running on Go

Six services in production, replacing slices of the PHP monolith. Without naming the internal repos:

- **Content scraping** — receives URL batches via gRPC, dispatches scrape tasks via NATS, applies results, streams content back to PHP via gRPC server-streaming. Owns its Postgres state, no shared DB with the monolith.
- **Provider execution arm** — receives scrape requests from NATS, talks to external providers (Zyte, Firecrawl, Google SERP, Yandex, DataForSEO, Wordstat), uploads raw payloads to object storage, publishes delivery events back. Independent service, polyglot-friendly bus contract.
- **Domain rule map** — replaces PHP's domain-rule logic. Owns rules, applies them on request via gRPC.
- **Dictionary replica** — async read-only replica of master dictionaries from PHP. Outbox + 3 NATS consumers per entity type. PHP-side stays authoritative for writes for now; reads are served from the Go replica.
- **Domain configuration service** — per-domain config served to sister services.
- **AI assistant** — self-hosted classifier / extractor on Ollama (Qwen, Mistral) + pgvector for RAG, with switchable LLM API backends (Anthropic, OpenAI, Google).
- **External gateway** (in progress) — partner-facing REST + gRPC, sitting in front of the internal Go services.

Each one runs on the [platform library](./platform.md), uses Snowflake IDs, exposes the standard observability surface, ships through the same CI pattern, and is supervised by the Rust sidecar that the registry tracks.

---

## What still lives in PHP — and that's fine

- Rich admin / business UX (specialised flows that Symfony does well).
- Long-tail legacy logic where the migration cost outweighs the savings.
- Some integrations with external systems where the PHP libraries are well-trodden.

The goal is **not** zero PHP. The goal is to put each domain on the language and stack that matches its constraints — and to do it with no flag day and no big-bang rewrite.

---

## Where the savings really come from

Memory reduction is the visible win. The structural wins are deeper:

- **Independent scaling.** A spike in scrape volume scales `content` and `provider` — not the whole monolith.
- **Independent deploy.** Pushing a fix to the dictionary replica does not redeploy the PHP monolith.
- **Independent recovery.** A crash loop in one Go service does not take down PHP HTTP traffic.
- **Smaller blast radius.** A bad migration in service X cannot corrupt service Y — there is no shared DB.
- **Backpressure-first.** NATS consumer pull limits naturally throttle producers, instead of retries cascading through the bus.
- **Less RAM in the cluster** = either fewer machines, or more headroom for actual product growth.

That's what "10× reduction" really means: not "the same workload now uses 1/10th the RAM", but **"the budget for the next 10× of product growth fits inside the current infra envelope"**.
