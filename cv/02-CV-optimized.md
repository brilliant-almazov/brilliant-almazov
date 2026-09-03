# ANTON BRILLIANTOV

**Senior Backend & Platform Engineer** · Distributed Systems · Real-Time Data at Scale
Ramat Gan, Israel · brilliantov.anton@gmail.com · [LinkedIn](https://www.linkedin.com/in/anton-brilliantov-53152714b/) · [GitHub](https://github.com/brilliant-almazov)

---

## Summary

I build the systems that other engineers build on — and I have run the product on top of them.

Twenty years in IT, 10+ writing production backends. I co-founded an SEO analytics SaaS, wrote ~70% of its backend, scaled it 40× from 30K to 1.3M+ daily queries per search engine, sold it to Ozon and M.Video, and exited after eight years. Since then: backend lead on a modular ecommerce engine, data architect cutting a client's cloud bill by up to 10×, and today the platform architect for a Go + Rust microservice platform progressively replacing a Symfony monolith — six bounded contexts in production in six months, on a two-engineer AI-first team.

Almost all of it has been the same shape of problem: data arriving faster than you would like, in volumes that punish sloppy design, in a system that has to stay correct and observable while it grows. I care about the load-bearing parts — schemas, migrations, queues, contracts, observability. I have also sat on the other side of the table: pricing, roadmap, the call about what *not* to build.

**What I want next:** a platform or architecture role where the hard part is the system, not the ticket queue. Distributed services, real-time data, analytics. Industry matters far less to me than the shape of the problem.

---

## Impact, measured

Same production workload, before and after each change. Not synthetic benchmarks.

| | Before | After | |
|---|---|---|---|
| Resident memory per worker | 100+ MB (Symfony daemon ~150 MB) | **~20 MB** per Go binary | **~7×** |
| Container image size | 100+ MB | **~20–30 MB** | **5–10×** |
| Process-manager footprint | ~50 MB supervisord | **~3 MB** Rust sidecar | **~17×** |
| Metrics scrape latency | 50–200 ms via Symfony | **sub-millisecond** via Rust bridge | **50–200×** |
| Cloud bill (BigQuery data layer) | baseline | **up to 10× lower** | **10×** |
| Client onboarding | 1–2 hours | **15 minutes** | **4–8×** |
| Query collection (Seowork) | 30,000/day | **1,300,000+/day** per search engine | **40×** |
| Time to production for a new service | ~1 week | **1 day** | **~5×** |

---

## What I bring

| | |
|---|---|
| **Platform engineering** | Shared Go library every service imports — resource lifecycle, gRPC/HTTP/Postgres/NATS/RabbitMQ/Redis wrappers, outbox, observability, test harness. 20+ repositories under one CI/CD pattern. |
| **Distributed systems** | Bounded contexts, Postgres outbox with at-least-once delivery, schema-first gRPC, NATS JetStream / RabbitMQ / Kafka, backpressure over retries, typed failure taxonomy. |
| **Data at scale** | 1.3M+ queries/day per engine collected, deduplicated, normalised, classified, scored and served. PostgreSQL schema design, partitioning, native ENUMs, pgx without an ORM. BigQuery pipelines with a 10× cost reduction. |
| **Product ownership** | Co-founder & CTO through to exit. Pricing, roadmap and scope negotiated directly with the CEO and with enterprise clients. I ship features that move a number, not tickets. |
| **Leadership** | Built a team from 1 to 10. Hiring, 1:1s, architecture review, on-call rota. Several juniors graduated into solid mids on my watch. |
| **Engineering velocity** | AI-augmented pipeline with hard guardrails: hooks-enforced conventions, 90% coverage floor in CI, real infrastructure in integration tests, never mocks. Speed that does not turn into debt. |

---

## Experience

### Senior Backend & Platform Engineer — *Stealth Startup (Malta)* · Contract · Remote
**Dec 2025 – present** · Marketing & SEO analytics SaaS

Sole platform architect on a two-engineer, AI-first team. Designing and shipping a Go + Rust microservice platform from scratch on top of a clean, domain-driven Symfony monolith — migrating for resource efficiency, not because the old code was bad.

- **Built the platform layer the whole company codes against** — a Go library every service imports: resource lifecycle, transport wrappers (gRPC, HTTP, Postgres, NATS, RabbitMQ, Redis), Postgres outbox, Snowflake IDs, structured logging, Prometheus metrics, testcontainers-based integration harness. **Time to production for a new microservice: one day instead of a week.**
- **Carved six bounded contexts out of the monolith into production Go services** — content scraping, provider execution, domain-rule mapping, dictionary replica, gateway, AI assistant, admin BFF. Each ships as several binaries (gRPC server, worker, outbox and scheduler processes). **Resident memory dropped ~7×, from 100+ MB per Symfony daemon to ~20 MB per Go binary**, and every domain became independently deployable, scalable and observable.
- **Replaced supervisord with a Rust sidecar** — a ~3 MB static musl binary, drop-in for existing configs, **~17× smaller** than the ~50 MB Python runtime it removed from every container.
- **Cut Prometheus scrape latency 50–200×** — from 50–200 ms through Symfony to sub-millisecond via a Rust bridge over Redis-backed PHP metrics, sustaining 12,500+ RPS with caching.
- **Shipped a Go control-plane registry** for cross-replica service discovery and a proxied admin API — single writer, mutual Ed25519 auth, push + pull heartbeat.
- **Built the operational control plane** — Go BFF plus a React (Mantine + Refine) admin panel covering RBAC, audit trail, soft-vs-hard delete and structured operations workflows. Direct database access by humans is forbidden by design; every privileged action is an audited workflow.
- **Made contracts a first-class artefact** — a shared Protocol Buffers repo as the single source of truth for every gRPC surface, with generated stubs for Go and PHP.
- **Owned CI/CD across 20+ repositories** — GitHub Actions on self-hosted runners, per-package coverage gates, binary- and image-size budgets enforced on every PR.
- **Made the quality bar mechanical, not cultural** — conventions codified per repo and enforced by tooling hooks, with a **90% coverage floor** and real Postgres, NATS and RabbitMQ in integration tests, never mocks for infrastructure.

`Go` `Rust` `PHP/Symfony` `PostgreSQL` `gRPC` `NATS` `RabbitMQ` `Redis` `BigQuery` `React + TypeScript` `Docker` `GCP` `GitHub Actions` `Prometheus/Grafana`

---

### Data Architect & BigQuery Consultant — *Independent consulting* · Part-time
**Sep 2023 – present** · Marketing analytics & SaaS backends

A separate, smaller engagement running alongside the role above — the data layer, where the money leaks.

- **Cut a client's cloud bill by up to 10×** by redesigning the BigQuery SQL and data layer: partitioning, clustering, materialised aggregates, and killing the full-scan queries that were quietly funding Google.
- **Compressed client onboarding from 1–2 hours to 15 minutes** by turning a manual launch checklist into an engineered workflow — the difference between a service that scales with headcount and one that doesn't.
- **Designing a SaaS backend that replaces Make/Zapier glue** with a real system: explicit contracts, retries, idempotency and observability instead of a chain of no-code webhooks nobody can debug.

References available on request.

`BigQuery` `PostgreSQL` `SQL` `GCP`

---

### Senior Backend Engineer / Team Lead — *Lenvendo*
**Nov 2021 – Aug 2023** · Modular ecommerce engine, later spun out as a SaaS

- **Designed the modular core of the engine** — clean Symfony layering with domain-driven module boundaries and async messaging over Kafka and RabbitMQ, so a new client vertical is a module rather than a fork.
- **Led the backend team of up to 6** — code review, hiring filter, mentorship. Several juniors became solid mids on my watch.
- **Worked the product side directly with PM and client** — roadmap, demos, technical specs and scope negotiation, including the unglamorous half: saying no to features that would have made the engine unmaintainable.

`PHP/Symfony` `PostgreSQL` `Redis` `RabbitMQ` `Kafka` `Kubernetes`

---

### Co-founder & CTO — *Seowork*
**Aug 2018 – Aug 2021** · SEO analytics SaaS · **successful exit**

Technical co-founder of the spin-out that turned the search analytics platform into a standalone SaaS, alongside the business founder, and CTO through to a successful exit in 2021 — eight years on the same product, from the first line of collection code in 2013 to the exit.

- **Wrote ~70% of the backend personally** — PHP first, then Go on the hot paths as volume outgrew the original design.
- **Scaled query collection 40×, from 30,000 to 1,300,000+ per day *per search engine*** — Google, Yandex and others each ran at that volume, with aggregate collection several times higher. No big-bang rewrite; the data layer was evolved deliberately, release by release, while the product stayed up.
- **Built the pipeline that consumed all of it** — ingestion, deduplication, normalisation, classification, scoring, materialised aggregates and retention. Collection was only half the system; turning raw results into reports clients trusted was the other half.
- **Won and kept enterprise clients including Ozon and M.Video** — their SEO teams ran daily decisions on our numbers, which set the reliability bar for everything we built.
- **Grew the team from 1 to 10** — 6–7 backend, 2–3 frontend, 1 QA — and owned hiring, 1:1s, architecture review and the on-call rota.
- **Owned the product, not just the stack** — pricing, roadmap and release strategy with the CEO, plus the database migration plans nobody else wanted to sign off on.

`PHP` `Go` `MySQL` `PostgreSQL` `Redis` `RabbitMQ`

---

### Head of Development — *404 Group*
**Jul 2015 – Jul 2018** · the same product, before the spin-out

Ran development on the search analytics product as it moved from internal agency tooling to a commercial platform with paying external clients.

- **Owned the backend end to end** — collection, storage, processing and reporting — and made the call on where the original design had to be replaced rather than patched as volume grew.
- **Built and led the engineering team** — hiring, code review, architecture decisions, release process. These were the first engineers of what became the SEOWORK team.
- **Took the product from an internal utility to a system outside companies paid for** and ran daily decisions on — the step that made the 2018 spin-out possible.

`PHP` `Go` `MySQL` `Redis` `RabbitMQ`

---

### Backend Developer, Search Analytics & Internal Tooling — *Webit*
**May 2013 – Jun 2015** · where the product started

Backend developer at a 100-person full-service digital agency (founded 2003, later ranked first among SEO agencies in the Ruward Award), on the in-house tooling the agency's own SEO department ran on.

- **Built the first version of the search-data collection backend** — rank and visibility data across Google and Yandex, collected daily across the agency's client portfolio, stored and served for analysts rather than for a dashboard demo.
- **Replaced hand-assembled client reporting with generated reports** — the same numbers, without an analyst spending a day per client per month.
- **Enterprise clients from the start** — even as agency tooling the platform served large ecommerce brands, and it was billed on the data itself, metered precisely. A wrong number was not a cosmetic bug, it was an invoice.
- **Cross-validation as a habit, not a QA step** — sources checked against each other before anything reached a report. Correctness of data was the product, and it has been the bar in everything I have built since.
- This codebase is the origin of the product I later co-founded and exited.

`PHP` `MySQL` `Redis`

---

### Developer, Corporate Reporting & Internal Systems — *NetByNet*
**Sep 2005 – Apr 2013** · 8 years · six roles · national ISP

Eight years at one company and six roles inside it. Joined a neighbourhood ISP a ten-minute walk from my flat, stayed through its acquisition by NetByNet — one of Russia's largest national providers — and ended up writing the reporting the business ran on.

- **Night-shift phone support, then day shift**, then field repairs at customer premises, then escalation and customer conflict resolution — the queue where the angry calls end up, and the first role where the outcome depended on judgement rather than a script.
- **Then network engineering** — network-level design and operations, then network engineer proper, followed by a year of internal technical support, where the users were the company's own departments and I learned what the business actually measured.
- **Final year and a half as a developer**, building the **corporate reporting decisions were made on**: IFRS and RAS financial reporting, revenue reporting, and KPI tooling for department heads and the board — plus custom call-centre software on Asterisk.

Analytics was not a later turn in my career. The first numbers executives decided on were queries I wrote.

Where I learned that the database is the soul of the product, and that most operational pain is a bad query wearing a costume.

---

## Writing

**"Breaking the Monolith"** — a 16-part technical series on dev.to and LinkedIn, written from inside the process rather than after it: zero-downtime cutover, identity ownership across services, distributed transactions and sagas, public versus internal gateways, Snowflake ID boundaries, platform-owned runtime, and how you test two systems that are supposed to agree while one replaces the other.

---

## Open source

- **[metrics-bridge-rs](https://github.com/brilliant-almazov/metrics-bridge-rs)** — Rust. Prometheus exporter over `promphp` Redis storage. **Sub-millisecond responses against 50–200 ms through PHP**, 12,500+ RPS with caching, verified across Redis 7/6, Dragonfly, Valkey and KeyDB.
- **[pgenum](https://github.com/brilliant-almazov/pgenum)** — Go. Zero-dependency runtime management of PostgreSQL `ENUM` types through plain `database/sql`. No ORM, no migration framework.
- **[railway-exporter-rs](https://github.com/brilliant-almazov/railway-exporter-rs)** — Rust. Prometheus exporter for Railway.app billing and usage metrics.

Full technical breakdown — architecture, platform design, quality standards, migration strategy: **[github.com/brilliant-almazov/brilliant-almazov](https://github.com/brilliant-almazov/brilliant-almazov)**

---

## Side product

**`redirector`** *(in development)* — my own SaaS: smart link redirection and traffic routing for marketing teams. Next.js front end, Symfony back end, built with the same discipline as the day job (outbox, explicit contracts, observability first). Product decisions, pricing and positioning included — I like keeping the founder muscle warm.

---

## Skills

**Languages** — Go (Golang) · Rust · PHP / Symfony · SQL · TypeScript
**Data** — PostgreSQL (schema design, partitioning, native ENUMs, pgx, forward-only migrations) · BigQuery · Redis · MySQL
**Messaging** — NATS JetStream · RabbitMQ · Kafka · Postgres outbox, at-least-once delivery
**APIs & contracts** — gRPC, schema-first Protocol Buffers · REST · BFF patterns
**Cloud & ops** — GCP (Artifact Registry, Cloud Run, BigQuery) · Docker · Kubernetes · Terraform · Railway · GitHub Actions self-hosted runners · Prometheus + Grafana
**Practice** — TDD and real-infrastructure integration testing (testcontainers) · CI quality gates · observability by default · AI-augmented development with enforced guardrails
**Front end** — React + TypeScript, Mantine, Refine, Next.js — enough to own the API contract end to end

---

## Certifications

Google Cloud — Modernizing Data Lakes & Data Warehouses · Building Resilient Streaming Analytics Systems · Modular Load Balancing with Terraform · Getting Started with GKE · Cloud SQL with Terraform

---

## Languages & location

**Russian** native · **English** professional working — fluent in written and technical communication (code review, docs, published technical writing), still sharpening spoken fluency · **Hebrew** beginner (Ulpan Aleph)

Based in **Ramat Gan, Israel**. Open to on-site, hybrid or remote. Here for the long term.

*Alpine skiing · psy-trance DJing.*
