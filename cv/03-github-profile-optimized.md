<h1 align="center">Anton Brilliantov</h1>

<p align="center">
  <strong>Senior Backend &amp; Platform Engineer — Distributed Systems · Real-Time Data at Scale</strong><br/>
  I build the platform other engineers build on — and I have run the product on top of it.<br/>
  20 years in IT · 10+ writing production backends · co-founder &amp; CTO of a SaaS through to exit
</p>

<p align="center">
  📍 <strong>Ramat Gan, Israel</strong> · 🟢 <strong>Open to senior backend / platform / architecture roles</strong><br/>
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

---

## In one paragraph

I co-founded an SEO analytics SaaS, wrote about seventy percent of its backend, scaled it from 30K to 1.3M+ daily queries per search engine, sold it to Ozon and M.Video, and exited after eight years. Since then I have led a backend team on a modular ecommerce engine, cut a client's cloud bill by up to 10× as a data architect, and today I am the platform architect for a Go + Rust microservice platform replacing a Symfony monolith — six bounded contexts in production in six months on a two-engineer team.

The through-line is not a language. It is one shape of problem: data arriving faster than you would like, in volumes that punish sloppy design, in a system that has to stay correct and observable while it grows. I like the load-bearing parts — schemas, migrations, queues, contracts, observability. And I have sat on the product side of the table too, which is why I argue about scope as hard as I argue about indexes.

**What I want next:** a platform or architecture role where the hard part is the system, not the ticket queue. Distributed services, real-time data, analytics. Industry matters far less to me than the shape of the problem.

---

## 🎯 What I'm building right now

**Since December 2025** — designing and shipping a microservice platform from scratch, Go + Rust, on top of an existing PHP / Symfony monolith. The product is a **marketing &amp; SEO analytics SaaS**: it crawls, classifies, scores and serves data about millions of pages, keywords and competitors.

The monolith is not tangled legacy. It is a well-modularised, domain-driven Symfony codebase — the kind of monolith that deserves to live. The migration is for **resource efficiency** (memory, image size, framework overhead), not code quality. That distinction shapes every decision below.

The team is two engineers. The team is AI-first. The bar is high, and it is enforced by machines rather than good intentions.

- **A Go platform library every service imports** — resource lifecycle, transport wrappers (gRPC, HTTP, Postgres, NATS, RabbitMQ, Redis), Postgres outbox, observability, Snowflake IDs, structured logging, a `testcontainers-go` integration harness. There is exactly one way to do everything, and a new microservice goes from empty repo to production in a day.
- **Six bounded contexts already carved out of the monolith** — content scraping, domain-rule mapping, dictionary replica, gateway, AI assistant, admin BFF. Each ships as several binaries (gRPC server, worker, outbox and scheduler processes). Resident memory fell from ~150 MB per Symfony daemon to ~20 MB per Go binary, and each domain became independently deployable, scalable and observable.
- **A Rust sidecar** — ~3 MB static musl binary replacing supervisord inside PHP containers. Drop-in for existing supervisord configs, ~17× smaller than the Python runtime it removed.
- **A Go control-plane registry** — cross-replica service discovery and a proxied admin API. Single writer, mutual Ed25519 auth, push + pull heartbeat.
- **An operational control plane** — Go BFF plus React (Mantine + Refine) admin, with RBAC, audit trail, soft-vs-hard delete and structured operations workflows. Humans never touch the database directly; every privileged action is an audited workflow.
- **Contracts as artefacts** — a shared Protocol Buffers repo as the single source of truth for every gRPC surface, generating stubs for Go and PHP.
- **CI/CD across 20+ repositories** — GitHub Actions on self-hosted runners, per-package coverage gates, binary- and image-size budgets enforced on every pull request.

> How the AI-augmented workflow stays honest — guardrails, hooks, review gates, and the volume numbers with the discipline that makes them safe: [`docs/ai-engineering.md`](docs/ai-engineering.md)

---

## 📚 Deep dives

Each document is self-contained, 150–300 lines, no filler.

| Document | What it covers |
|---|---|
| [**`docs/architecture.md`**](docs/architecture.md) | The distributed system map — layers, surfaces, ASCII topology, the outbox → NATS sequence. |
| [**`docs/platform.md`**](docs/platform.md) | The platform abstractions — Go library, Rust sidecar, control-plane registry, service template, and how a new microservice ships in a day. |
| [**`docs/admin-operations.md`**](docs/admin-operations.md) | Admin as a platform-wide control plane — why direct DB access is forbidden, and how RBAC, audit, soft-vs-hard delete and operations workflows fit together. |
| [**`docs/migration.md`**](docs/migration.md) | PHP → Go migration — the reasoning, the method, what is measured, what deliberately stays in PHP, and where the savings actually come from. |
| [**`docs/ai-engineering.md`**](docs/ai-engineering.md) | AI-augmented engineering — skills, hooks, sub-agents, persistent memory, and the honest thesis about where the model helps and where it must not decide. |
| [**`docs/quality-standards.md`**](docs/quality-standards.md) | The enforced rule-book — Go, frontend, database, SQL, observability, process. |
| [**`docs/refactoring-plans.md`**](docs/refactoring-plans.md) | Live refactoring plans — the admin strangler split and the platform worker abstraction. |

---

## 💼 Career

### 🧱 Senior Backend &amp; Platform Engineer · Stealth startup (Malta) · contract, remote
**Dec 2025 – present** · marketing &amp; SEO analytics SaaS · two-engineer AI-first team

Sole platform architect. Everything in the section above is mine end to end — the platform library, the six extracted domains, the Rust sidecar, the control plane, the admin surface, the CI estate and the quality gates.

**Stack:** Go · Rust · PHP / Symfony · PostgreSQL · gRPC · NATS · RabbitMQ · Redis · BigQuery · React + TypeScript · Docker · GCP · GitHub Actions · Prometheus + Grafana

---

### 🛠 Data Architect &amp; BigQuery Consultant · independent · part-time
**Sep 2023 – present** · marketing analytics &amp; SaaS backends

A separate, smaller engagement alongside the role above — the data layer, where the money leaks.

- **Up to 10× cloud cost reduction** for the client: partitioning, clustering, materialised aggregates, and the removal of full-scan queries that were quietly funding Google.
- **Client onboarding from 1–2 hours to 15 minutes** — a manual launch checklist turned into an engineered workflow. The difference between a service that scales with headcount and one that doesn't.
- **Designing a SaaS backend to replace Make / Zapier glue** with explicit contracts, retries, idempotency and observability, instead of a chain of no-code webhooks nobody can debug at 2am.

---

### 🚀 Co-founder &amp; CTO · Seowork
**Jun 2013 – Aug 2021** · 8 years · SEO analytics SaaS · **exited 2021**

From an empty repository to a load-bearing tool inside the largest Russian-speaking ecommerce companies.

- **Wrote ~70% of the backend personally** — PHP first, then Go on the hot paths as volume outgrew the original design.
- **Scaled collection 40×, from 30,000 to 1,300,000+ queries per day *per search engine*.** Google, Yandex and others each ran at that volume; aggregate collection was several times higher. No big-bang rewrite — the data layer was evolved release by release while the product stayed up.
- **Built the pipeline that consumed all of it** — ingestion, deduplication, normalisation, classification, scoring, materialised aggregates, retention. Collection was half the system; turning raw results into numbers clients would bet decisions on was the other half.
- **Won and kept enterprise clients including Ozon and M.Video**, whose SEO teams made daily calls on our data — which set the reliability bar for everything else.
- **Grew the team from one to ten** — 6–7 backend, 2–3 frontend, 1 QA — owning hiring, 1:1s, architecture review and the on-call rota.
- **Owned the product, not just the stack** — pricing, roadmap and release strategy with the CEO, and the database migration plans nobody else wanted to sign.

**Stack:** PHP · Go · MySQL / PostgreSQL · Redis · RabbitMQ

---

### 🏢 Senior Backend Engineer / Team Lead · Lenvendo
**Nov 2021 – Aug 2023** · modular ecommerce engine, later spun out as a SaaS

- **Designed the modular core** — clean Symfony layering, domain-driven module boundaries, async over Kafka and RabbitMQ, so a new client vertical is a module rather than a fork.
- **Led a backend team of up to 6** — code review, hiring filter, mentorship. Several juniors graduated into solid mids.
- **Worked the product side directly with PM and client** — roadmap, demos, specs, scope negotiation, including the unglamorous half: refusing features that would have made the engine unmaintainable.

**Stack:** PHP / Symfony · PostgreSQL · Redis · RabbitMQ · Kafka · Kubernetes

---

### 📞 Developer, Corporate Reporting &amp; Internal Systems · NetByNet
**2005 – Apr 2013** · 8 years · national ISP

Eight years at one company, from the phone to the codebase — call-centre operator, field service, customer-facing and internal technical support, then development.

As a developer I built the **corporate reporting systems the company's business analysts ran on**: IFRS and RAS financial reporting, KPI tooling, and custom call-centre software on Asterisk. Analytics and data have been the through-line since the start of the career, not a recent turn.

Where I learned that the database is the soul of the product, and that most operational pain is a bad query wearing a costume.

---

## 🏗 Stack &amp; what I actually do with it

| Layer | What I do with it |
|---|---|
| **Go** | Platform library imported by every service — resource lifecycle, transport wrappers, outbox, Snowflake IDs, structured logging, Prometheus metrics, `testcontainers-go` harness. Six production services. |
| **Rust** | Process-manager sidecar (~3 MB static binary, drop-in supervisord replacement). Prometheus exporters answering in **sub-millisecond** time against 50–200 ms through PHP. |
| **PHP / Symfony** | 15+ years, from the inside out. Decomposed legacy monoliths and shipped clean modular codebases — the reason I can migrate one without breaking it. |
| **PostgreSQL** | Schema design, partitioning, INET and native ENUM types, `pgx` without an ORM, forward-only `goose` migrations, outbox with a NATS publisher. Wrote [`pgenum`](https://github.com/brilliant-almazov/pgenum). |
| **BigQuery** | Analytical pipelines and the SQL layer behind them. 10× cloud cost reduction for a client; launch workflows 4–8× faster. |
| **gRPC** | Proto-first service contracts in a shared repo. Server streaming for content delivery, unary for control APIs, domain-aware error envelopes. |
| **NATS / RabbitMQ / Kafka** | NATS JetStream with Postgres outbox integration in Go; RabbitMQ and Kafka on the PHP side. Backpressure over retries. |
| **Redis** | Caching, rate limiting, session storage, and a direct reader for PHP-side Prometheus metrics. |
| **React + TypeScript** | Admin panels (Mantine v7 + Refine) over Go BFFs. I own the API contract and the React ↔ Go data flow. |
| **Cloud &amp; ops** | GCP (Artifact Registry, Cloud Run, BigQuery), Railway, Docker, Kubernetes, GitHub Actions with self-hosted runners, Prometheus + Grafana. |

---

## 🌐 Open source

- **[metrics-bridge-rs](https://github.com/brilliant-almazov/metrics-bridge-rs)** — Rust. Prometheus exporter over `promphp/prometheus_client_php` Redis storage. **Sub-millisecond responses against 50–200 ms through PHP**, 12,500+ RPS with caching, verified across Redis 7/6, Dragonfly, Valkey and KeyDB. README in 18 languages.
- **[pgenum](https://github.com/brilliant-almazov/pgenum)** — Go. Zero-dependency runtime management of PostgreSQL `ENUM` types through plain `database/sql`. No ORM, no migration framework required.
- **[railway-exporter-rs](https://github.com/brilliant-almazov/railway-exporter-rs)** — Rust. Prometheus exporter for Railway.app billing and usage metrics.

---

## 🧪 Building on the side

**`redirector`** *(in development)* — my own SaaS: smart link redirection and traffic routing for marketing teams. Next.js front end, Symfony back end, built with the same discipline as the day job — Postgres outbox, explicit contracts, observability first. Pricing and positioning included; I like keeping the founder muscle warm.

**Design notes** — RFCs for things that haven't shipped, including a geo-distributed Rust scraper with batch and interactive modes. Idea stage, honestly labelled as such.

---

## 🧠 Engineering principles, one screen

Full rule-book in [`docs/quality-standards.md`](docs/quality-standards.md). The short version:

- **Interface-driven Go, OOP discipline.** No procedural helpers. Transactions are struct fields, not function arguments. One struct per file, 100 lines maximum.
- **`errors.Is` / `errors.As` only.** Never direct comparison, never a type switch on errors.
- **Observability is not bolted on.** Every driver, pool and client publishes counters and histograms per operation, from the platform library.
- **90% line coverage minimum, enforced in CI.** Floors ratchet up, never down. Below the floor, the PR does not merge.
- **Real integration tests.** `testcontainers-go`, one container per run, namespace-isolated data per test. Never mocks for infrastructure.
- **A flaky test is a broken test.** 48-hour quarantine, then fixed or deleted.
- **Schema-first contracts.** Shared proto repo, forward-only migrations, `COMMENT ON COLUMN` on every column, Snowflake IDs — never `SERIAL`, never `UUID` on a hot path.
- **Zero defaults in shared libraries.** The caller passes every config value. Forget one and the service fails to start — not in production three weeks later.
- **AI helps good engineers ship faster, and bad engineers ship bad code faster.** The model is good at execution and bad at judgement. Architecture goes through me.

---

## 🌌 The part that doesn't fit on a CV

Twenty years in, I have the thing engineers call **taste** — sometimes intuition, sometimes just feel. I can usually sense that a design is wrong before I can articulate why, and by the next morning I have the argument. I love this craft enough to be picky about it, and I keep learning because every honest hour at the keyboard sharpens that feel a little further.

Unusual thing to write on a profile. Earned thing to say.

---

## 🎓 Background, languages, life

**Languages** — **Russian** native · **English** professional working: I read, write and review in English every day and I am comfortable in technical discussion, docs and async work; spoken fluency is the part I am still sharpening, and I am investing in it · **Hebrew** beginner (Ulpan Aleph), and I am here for the long term.

**Background** — no CS degree. Twenty years in IT and 10+ years of production code instead, including a SaaS I built, led and exited. The systems are the credential; several of them are linked above.

**Life** — alpine skiing and psy-trance DJing.

---

## 📫 Hiring me

I am based in **Ramat Gan, Israel**, looking for a senior **backend / platform / architecture** role. On-site, hybrid or remote. Strong preference for teams that take the boring parts seriously — observability, migrations, contracts, the data layer.

What you get: an engineer who has designed the platform *and* owned the P&amp;L on top of it, who ships fast without leaving debt behind, and who will tell you plainly when a plan is wrong.

- ✉️ **Email:** [brilliantov.anton@gmail.com](mailto:brilliantov.anton@gmail.com)
- 💼 **LinkedIn:** [anton-brilliantov-53152714b](https://www.linkedin.com/in/anton-brilliantov-53152714b/)
- 🐙 **GitHub:** [@brilliant-almazov](https://github.com/brilliant-almazov)

<p align="center"><sub>Last updated: September 2026</sub></p>
