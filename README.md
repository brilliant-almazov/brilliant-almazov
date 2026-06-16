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
    <img src="https://skillicons.dev/icons?i=go,rust,php,symfony,ts,react,nextjs,postgres,redis,nats,rabbitmq,kafka,gcp,docker,kubernetes,grafana,prometheus,grpc,linux,git,github" alt="stack" />
  </a>
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=brilliant-almazov&show_icons=true&theme=tokyonight&include_all_commits=true&count_private=true&hide_border=true" alt="stats" height="160" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=brilliant-almazov&layout=compact&theme=tokyonight&hide=html,css,scss,roff&hide_border=true" alt="top langs" height="160" />
</p>

<p align="center">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=brilliant-almazov&theme=tokyonight&hide_border=true" alt="streak" height="160" />
</p>

---

## 🎯 What I'm doing right now

**Since December 2025**, I've been designing and shipping a microservice platform from scratch — Go + Rust on top of an existing PHP / Symfony monolith. The product is a **marketing & SEO analytics SaaS in the gaming vertical**: it crawls, classifies, scores and serves data about millions of pages, keywords and competitors.

The team is small. The team is AI-first. The bar is high.

- A **Go platform library** every service imports — resource lifecycle, transport wrappers (gRPC, HTTP, Postgres, NATS, RabbitMQ, Redis), Postgres outbox, observability, Snowflake IDs, structured logging, integration-test harness.
- A **Rust sidecar** — static ~3 MB binary that replaces supervisord inside PHP containers. Drop-in for existing supervisord configs. Replaced a ~50 MB Python runtime per container.
- A **Go control-plane registry** — single writer, mutual Ed25519 auth, push + pull heartbeat, reverse-proxy admin API across replicas.
- **Six Go microservices in production** — content scraping, domain-rule mapping, dictionary replica, gateway, AI assistant, admin BFF. Each replaces a slice of the PHP monolith and drops resident memory from **100+ MB per PHP worker (a typical Symfony daemon sits around ~150 MB) to ~20 MB per Go binary**.

> Headline numbers: **22 active repositories · 6,300+ commits · ~3.4 M lines of source authored in 6.5 months · ~32 commits / day**.
> Detail in [`docs/ai-engineering.md`](docs/ai-engineering.md).

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

### 🛠 Freelance / Product consulting · Data architect & BigQuery expert
**Sep 2023 – present** · with [Natan Kreiderman](https://www.linkedin.com/in/natan-kreiderman/)

Marketing analytics and SaaS backends for the gaming industry. Started as BigQuery and data-layer consulting; since **December 2025**, designing and shipping the full microservice platform described above.

- Designed a systematic SQL & data layer in **BigQuery** — **up to 10× cloud cost reduction** for the client.
- Accelerated client launch workflow from **1–2 hours down to 15 minutes**.
- Designing a SaaS backend that replaces Make / Zapier glue with a real engineered system.
- Built the Go platform library, the Rust sidecar, the Go registry and six production Go services from scratch.

### 🚀 Seowork · Co-founder & CTO
**Jun 2013 – Aug 2021** · 8 years · **successful exit**

Built an SEO analytics SaaS from a blank repo into a load-bearing tool for the largest Russian-speaking ecommerce companies. Exited the company in 2021 after 8 years.

- **Wrote ~70 % of the backend personally** in PHP, later Go for hot paths.
- **Scaled from 30,000 to 1,300,000+ daily queries** — 40× growth handled with no big-bang rewrites, just careful evolution of the data layer.
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
- **Real integration tests.** `testcontainers-go` — one container per test run, namespace-isolated data per test. Never mocks for infrastructure.
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
