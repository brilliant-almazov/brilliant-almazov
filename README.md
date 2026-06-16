<h1 align="center">Anton Brilliantov</h1>

<p align="center">
  <strong>Senior backend engineer — PHP · Go · Rust · PostgreSQL · BigQuery</strong><br/>
  10+ years building data-heavy platforms · ~20 years in IT<br/>
  Currently designing a Go + Rust microservice platform that replaces a PHP / Symfony monolith — service by service, with discipline.
</p>

<p align="center">
  📍 <strong>Ramat Gan, Israel</strong> · 🟢 <strong>Open to work — senior backend / platform role in Israel</strong><br/>
  ✉️ <a href="mailto:brilliantov.anton@gmail.com">brilliantov.anton@gmail.com</a> · 💼 <a href="https://www.linkedin.com/in/anton-brilliantov-53152714b/">LinkedIn</a> · 🐙 <a href="https://github.com/brilliant-almazov">GitHub</a>
</p>

<p align="center">
  <a href="https://skillicons.dev">
    <img src="https://skillicons.dev/icons?i=go,rust,php,symfony,ts,react,nextjs,postgres,redis,kafka,gcp,docker,kubernetes,grafana,prometheus,linux,git,github" alt="stack" />
  </a>
</p>

<p align="center">
  <img src="https://shields.io/badge/NATS-27AAE1?style=flat&logo=natsdotio&logoColor=white" alt="NATS" />
  <img src="https://shields.io/badge/RabbitMQ-FF6600?style=flat&logo=rabbitmq&logoColor=white" alt="RabbitMQ" />
  <img src="https://shields.io/badge/gRPC-244c5a?style=flat&logo=google&logoColor=white" alt="gRPC" />
  <img src="https://shields.io/badge/BigQuery-669DF6?style=flat&logo=googlebigquery&logoColor=white" alt="BigQuery" />
  <img src="https://shields.io/badge/PostgreSQL-336791?style=flat&logo=postgresql&logoColor=white" alt="PostgreSQL" />
</p>

<p align="center">
  <img src="https://streak-stats.demolab.com/?user=brilliant-almazov&theme=tokyonight&hide_border=true&date_format=j%20M%5B%20Y%5D" alt="streak" height="180" />
</p>

### 📊 Real language breakdown (private + public, Dec 2025 → Jun 2026)

GitHub's top-langs card only counts *public* repositories — which under-represents PHP (the production Symfony monolith is private) and over-represents Rust (where the open-source projects live). The honest distribution, measured across **all** active repos by net source LOC, is:

| Language | Share | |
|---|---:|---|
| **PHP** (Symfony monolith — still active, in migration) | **~55%** | ![](https://geps.dev/progress/55?dangerColor=8993be&warningColor=8993be&successColor=8993be) |
| **Go** (platform library, 6 microservices, BFF) | **~30%** | ![](https://geps.dev/progress/30?dangerColor=00add8&warningColor=00add8&successColor=00add8) |
| **TypeScript / React** (admin UI, BFF clients) | **~8%** | ![](https://geps.dev/progress/8?dangerColor=3178c6&warningColor=3178c6&successColor=3178c6) |
| **SQL / Proto / YAML / Markdown** (migrations, schemas, IaC, docs) | **~4%** | ![](https://geps.dev/progress/4?dangerColor=336791&warningColor=336791&successColor=336791) |
| **Rust** (sidecar + OSS exporters) | **~3%** | ![](https://geps.dev/progress/3?dangerColor=dea584&warningColor=dea584&successColor=dea584) |

> **Headline numbers (same period):** 🗂 **22 active repositories** · 📝 **6,300+ commits** · ➕ **~3.4 M lines of source** · ⏱ **~32 commits / day** · 🚀 **6 bounded contexts** carved out of the PHP monolith into Go microservices (multiple binaries per domain — servers, workers, runners) · 📦 **3 public OSS libraries shipped**.

---

## 🎯 What I'm doing right now

**Since December 2025**, I've been designing and shipping a microservice platform from scratch — Go + Rust on top of an existing PHP / Symfony monolith. The product is a **marketing & SEO analytics SaaS in the gaming vertical**: it crawls, classifies, scores and serves data about millions of pages, keywords and competitors.

The team is small. The team is AI-first. The bar is high.

- A **Go platform library** every service imports — resource lifecycle, transport wrappers (gRPC, HTTP, Postgres, NATS, RabbitMQ, Redis), Postgres outbox, observability, Snowflake IDs, structured logging, integration-test harness.
- A **Rust sidecar** — static ~3 MB binary that replaces supervisord inside PHP containers. Drop-in for existing supervisord configs. Replaced a ~50 MB Python runtime per container.
- A **Go control-plane registry** — single writer, mutual Ed25519 auth, push + pull heartbeat, reverse-proxy admin API across replicas.
- **Six bounded contexts already carved out of the PHP monolith** — content scraping, domain-rule mapping, dictionary replica, gateway, AI assistant, admin BFF. Each domain ships as **one or more Go microservices** (typically a gRPC server + a worker binary; some have additional outbox / scheduler / sidecar processes). Net effect: resident memory drops from **100+ MB per PHP worker (a typical Symfony daemon sits around ~150 MB) to ~20 MB per Go binary**, and the domain becomes independently scalable, deployable and observable.

> Detail on AI-augmented workflow + per-repo activity: [`docs/ai-engineering.md`](docs/ai-engineering.md).

---

## 📚 Deep dives

The story is split into focused documents — each one self-contained, ~150–300 lines, no fluff.

| Document | What it covers |
|---|---|
| [**`docs/architecture.md`**](docs/architecture.md) | The distributed system map. Layers, surfaces, ASCII topology, outbox + NATS sequence. |
| [**`docs/platform.md`**](docs/platform.md) | The platform abstractions. Go library, Rust sidecar, Go registry, service template — how a new microservice ships in a day. |
| [**`docs/admin-operations.md`**](docs/admin-operations.md) | Admin as platform-wide operational control plane. Why direct DB access is forbidden, how RBAC / audit / soft-vs-hard delete / operations workflows work. |
| [**`docs/migration.md`**](docs/migration.md) | PHP → Go migration. Why, how, what's measured, what stays in PHP, where the savings actually come from. |
| [**`docs/ai-engineering.md`**](docs/ai-engineering.md) | AI-augmented engineering. Skills, hooks, sub-agents, persistent memory, productivity metrics, the honest thesis on AI in engineering. |
| [**`docs/quality-standards.md`**](docs/quality-standards.md) | Hard quality standards enforced by hooks. Universal + Go + Frontend + Database + SQL + Observability + Process. |
| [**`docs/refactoring-plans.md`**](docs/refactoring-plans.md) | Active refactoring plans: admin strangler split (5 services + UI), platform worker abstraction (6 patterns, 1 pipeline). |

---

## 💼 Career timeline

### 🧱 Stealth Startup (Malta) · Senior backend & platform engineer · Contract
**End of December 2025 – present** · **main current engagement** · **super small AI-first team** · remote from Israel

A Malta-based stealth startup. **Marketing & SEO analytics in the gaming vertical.** This is the engagement I spend the majority of my time on right now — designing and shipping a new Go + Rust microservice platform from scratch, in a team that is two engineers small and AI-first by design.

> ⚙️ **What I'm building** — a polyrepo distributed system that augments and progressively replaces a clean, domain-driven PHP / Symfony monolith. The monolith is not a tangled legacy: it is a well-modularised, best-practices Symfony codebase, the kind of monolith that actually deserves to live. The migration to Go and Rust is for **resource efficiency** (memory, image size, framework overhead), **not code quality**.

**What I've personally designed and shipped in 6.5 months:**

- A **Go platform library** every new service imports — resource lifecycle, gRPC / HTTP / Postgres / NATS / RabbitMQ / Redis wrappers, Postgres outbox, observability, Snowflake IDs, structured logging, `testcontainers-go` integration-test harness. Defines *one way* to do everything.
- A **Rust sidecar** (~3 MB static musl binary) replacing supervisord inside PHP containers — drop-in for existing supervisord configs, **~17× reduction** in process-manager footprint vs the old Python supervisord (~50 MB).
- A **Go control-plane registry** for cross-replica service discovery and proxied admin API (mutual Ed25519, push + pull heartbeat).
- **Six bounded contexts already extracted from the PHP monolith** — content scraping, domain-rule mapping, dictionary replica, gateway, AI assistant, BFF/admin API. Each domain runs as one or more Go microservices (server + worker + supporting processes); the total binary count is higher than six.
- A **Go BFF + React (Mantine + Refine) admin panel** — the operational control plane for the whole stack (RBAC, audit, soft-vs-hard delete, structured operations workflows).
- A **shared Protocol Buffers schema repo** — single source of truth for all gRPC contracts; generated stubs for Go and PHP.
- **CI / CD** across 20+ repos: GitHub Actions self-hosted runners, coverage gates per package, binary-size badges, image-size badges, version badges.

**Stack:** Go · Rust · PHP / Symfony · PostgreSQL · gRPC · NATS · RabbitMQ · Redis · BigQuery · React + TypeScript · Docker · GCP · GitHub Actions · Prometheus + Grafana.

**Quality discipline that makes the speed honest:**

- Interface-driven Go, OOP, one struct per file, max 100 lines per file.
- `errors.Is` / `errors.As` only — never direct comparison or type switch.
- Forward-only migrations, Snowflake IDs everywhere, `COMMENT ON COLUMN` required.
- **90 %+ test coverage floor enforced in CI**; real integration tests against real Postgres / NATS / RabbitMQ in `testcontainers-go` — never mocks for infrastructure.
- No flaky-test culture; per-driver Prometheus metrics; structured zap logs; observability baked into the platform library, not bolted on.
- All of the above is **codified in per-repo `CLAUDE.md` files and enforced by `PreToolUse` / `PostToolUse` hooks** — AI cannot drift, humans cannot forget.

**Team & throughput.** The team is tiny. The codebase is large and growing fast. **6,300+ commits, 3.4 M lines of source authored in 6 months, ~32 commits / day.** The discipline above is the reason that volume doesn't become technical debt. See [`docs/ai-engineering.md`](docs/ai-engineering.md) for the AI-augmented engineering practices and [`docs/quality-standards.md`](docs/quality-standards.md) for the full quality rule-book.

---

### 🛠 Freelance / Product consulting · Data architect & BigQuery expert
**Sep 2023 – present** · ongoing in a *reduced* capacity, alongside the Stealth Startup engagement above · with [Natan Kreiderman](https://www.linkedin.com/in/natan-kreiderman/)

A separate, smaller consulting track. Marketing analytics and SaaS backends — primarily on the data layer.

- Designed a systematic SQL & data layer in **BigQuery** — **up to 10× cloud cost reduction** for the client.
- Accelerated client launch workflow from **1–2 hours down to 15 minutes**.
- Designing a SaaS backend that replaces Make / Zapier glue with a real engineered system.

> Distinct engagement, distinct client, distinct codebase — *not* the Stealth Startup work above.

### 🚀 Seowork · Co-founder & CTO
**Jun 2013 – Aug 2021** · 8 years · **successful exit**

Built an SEO analytics SaaS from a blank repo into a load-bearing tool for the largest Russian-speaking ecommerce companies. Exited the company in 2021 after 8 years.

- **Wrote ~70 % of the backend personally** in PHP, later Go for hot paths.
- **Scaled query collection from 30,000 to 1,300,000+ daily queries — *per search engine*.** Google, Yandex and other engines each ran at that volume; aggregate daily collection was several times higher. 40× growth handled with no big-bang rewrites, just careful evolution of the data layer.
- **Built the downstream pipeline that consumed all of that** — ingestion, deduplication, normalisation, classification, scoring, materialised aggregates, retention. The collection volume was only half the system; processing those results into reports and dashboards was the other half, and it was just as engineered.
- **Clients:** Ozon, M.Video, and other top-tier ecommerce.
- Built and led the team: 6–7 backend, 2–3 frontend, 1 QA. Hiring, 1:1s, architecture reviews, on-call rota.
- Owned everything from product strategy with the CEO to migration plans for the database.
- **Stack:** PHP, Go (partial), MySQL / PostgreSQL, Redis, RabbitMQ.

### 🏢 Lenvendo · Senior backend engineer / Team lead
**Nov 2021 – Aug 2023**

Modular ecommerce engine, later spun out as a SaaS. Backend lead on a team of up to 6.

- Designed the modular core of the engine: clean Symfony layering, domain-driven module boundaries, async via Kafka and RabbitMQ.
- Led the backend team — code reviews, hiring filter, mentorship. Several juniors graduated into solid mids on my watch.
- Worked directly with PM and the client — roadmap, demos, technical specs, scope negotiation.
- **Stack:** PHP / Symfony, PostgreSQL, Redis, RabbitMQ, Kafka, Kubernetes.

### 📞 NetByNet · Developer · BI systems
**2005 – Apr 2013** · 8 years

Started in tech support, moved into development. Internal reporting and KPI tools, custom call-centre software. Where I learned that databases are the soul of any product, and bad SQL is the source of most operational pain.

---

## 🏗 Stack & impact

| Layer | What I do with it |
|---|---|
| **PHP / Symfony** | 15+ years. Symfony from the inside out. Decomposed legacy monoliths, shipped clean modular codebases. |
| **Go** | Designed a platform library imported by every service. Resource lifecycle, transport wrappers, outbox, Snowflake IDs, structured logging, Prometheus metrics, `testcontainers-go` harness. Six production services. |
| **Rust** | Process-manager sidecar (~3 MB static binary, drop-in supervisord replacement). Prometheus exporters with **sub-millisecond responses** vs 50–200 ms through PHP. |
| **PostgreSQL** | Schema design, partitioning, INET / native ENUM types, `pgx` (no ORM), `goose` forward-only migrations, outbox pattern with NATS publisher, Snowflake IDs everywhere. Wrote [`pgenum`](https://github.com/brilliant-almazov/pgenum) — runtime PG enum management. |
| **BigQuery** | Designed analytical pipelines and the SQL layer behind them. **10× cloud cost reduction** for a client. Launch workflows accelerated 4–8×. |
| **gRPC** | Service-to-service contracts, proto-first, shared proto repo. Server-streaming for content delivery, unary for control APIs, domain-aware error envelopes. |
| **NATS / RabbitMQ / Kafka** | NATS JetStream for modern Go services with Postgres outbox integration. RabbitMQ + Kafka in the PHP world. Backpressure over retries. |
| **Redis** | Caching, rate limiting, session storage. Direct reader for PHP-side Prometheus metrics. |
| **React + TypeScript** | Admin panels (Mantine v7 + Refine.dev) over Go BFFs. I own the API contract and the React↔Go data flow. |
| **Cloud & ops** | GCP (Artifact Registry, Cloud Run, BigQuery), Railway, Docker, GitHub Actions (self-hosted runners), Prometheus + Grafana, Kubernetes. |

---

## 🌐 Open-source

- **[metrics-bridge-rs](https://github.com/brilliant-almazov/metrics-bridge-rs)** — Rust. Fast Prometheus exporter on top of `promphp/prometheus_client_php` Redis storage. **Sub-millisecond responses** vs 50–200 ms through PHP. Tested across Redis 7/6, Dragonfly, Valkey, KeyDB. 12,500+ RPS with caching. Multi-language README (18 languages).
- **[pgenum](https://github.com/brilliant-almazov/pgenum)** — Go. Zero-dependency library for managing PostgreSQL `ENUM` types at runtime through the standard `database/sql` interface. No ORM, no migrations needed.
- **[railway-exporter-rs](https://github.com/brilliant-almazov/railway-exporter-rs)** — Rust. Prometheus exporter for Railway.app billing & usage metrics.

---

## 🧪 Personal R&D

- **`redirector`** *(in progress)* — a personal SaaS in development. Smart link-redirection and traffic-routing tool for marketing — Next.js frontend, Symfony backend. Structured as a small platform of its own, applying the same patterns (Postgres outbox, gRPC contracts, observability-first) that I use at work.
- **Design notes** — drafts and RFCs for ideas that haven't shipped yet (a geo-distributed Rust scraper with batch + interactive modes is one of them). Idea-stage, not production.

---

## 🧠 Engineering principles in one screen

For the *full* rules-of-engagement (Go, frontend, DB, SQL, observability, process), see [`docs/quality-standards.md`](docs/quality-standards.md). The short version:

- **Interface-driven Go, OOP discipline.** No procedural helpers. Transactions are struct fields, not function arguments. One struct per file. Max 100 lines per file.
- **`errors.Is` / `errors.As` only.** Never direct comparison or type switch on errors.
- **No bolt-on observability.** Every driver, pool, client publishes Prometheus counters and histograms per operation.
- **Tests on everything, 90 % line coverage minimum, enforced by CI.** Floors only ratchet up, never down. Below floor → PR blocked.
- **Real integration tests.** `testcontainers-go` — one container per test run, namespace-isolated data per test. Never mocks for infrastructure.
- **No flaky-test culture.** A flaky test is a broken test. 48 h quarantine maximum, then fix or delete.
- **Schema-first contracts.** Shared proto repo. Migrations forward-only with a `COMMENT ON COLUMN` for every column. Snowflake IDs everywhere — never `SERIAL`, never `UUID` on the hot path.
- **Zero defaults in shared libraries.** The caller passes every config value. If they forget, the service fails to start — not in production three weeks later.
- **AI helps good engineers ship faster. AI helps bad engineers ship bad code faster.** The model is best at execution, not judgement. Every architectural decision goes through me. See [`docs/ai-engineering.md`](docs/ai-engineering.md).

---

## 🎓 Education, languages, life

- **Languages — honest version:**
  - **Russian** — native.
  - **English** — not my strongest side. I read, write and review code in English every day, and I'm comfortable on technical Slack / GitHub / docs. **Speaking is the weakest part** — I can hold technical conversations and code reviews, but I'm not fluent in casual / sales-style English. It's improving, and I'm willing to invest in it (formal lessons, paired-speaking, whatever the team uses). If the team is OK with a tech-focused English level today, the rest will catch up.
  - **Hebrew** — A1 (Ulpan Aleph). Beginner. Climbing slowly. I'm clear-eyed about it: not a working language for me yet, but I live in Israel and I'm in for the long term.
- **Education:** medical school basics, 2004 — not relevant. **No CS degree.** Everything since is self-taught and field-tested across 20 years in IT and 10+ years writing production code. The work speaks louder than the diploma I don't have.
- **Hobbies:** alpine skiing, DJing psy-trance.

---

## 📫 Hire me

I'm **based in Ramat Gan, Israel** and looking for a senior **backend / platform / data-infrastructure** role here. Open to on-site, hybrid or remote. Strong preference for teams that take the boring parts of the stack seriously — observability, migrations, infrastructure, the data layer.

**Honest notes for hiring managers:**

- ✅ I will out-engineer most candidates on PHP, Go, Rust, PostgreSQL and BigQuery.
- ✅ I've built and exited a SaaS, led teams, and shipped real systems for 20 years.
- ⚠️ My **spoken English is intermediate**, not native. Technical comms and async work — no problem. Live customer-facing presentations in English — not yet. I will keep working on it; I won't pretend it's already there.
- ⚠️ My **Hebrew is A1**. If your team works in Hebrew day-to-day, I'll need a runway to get there. If it works in English / Russian / a mix — I'm operational from day one.
- ✅ I'm not looking for a tourist role. **I'm in Israel to stay**, and I'm looking for a team I can grow with.

- ✉️ **Email:** [brilliantov.anton@gmail.com](mailto:brilliantov.anton@gmail.com)
- 💼 **LinkedIn:** [anton-brilliantov-53152714b](https://www.linkedin.com/in/anton-brilliantov-53152714b/)
- 🐙 **GitHub:** [@brilliant-almazov](https://github.com/brilliant-almazov)

<p align="center"><sub>Last updated: June 2026 · Stats above are auto-generated from public + private contributions.</sub></p>
