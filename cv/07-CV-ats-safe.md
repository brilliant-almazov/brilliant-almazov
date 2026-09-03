# ATS-safe версия резюме

**Как пользоваться.** Скопировать текст ниже в Google Docs или Word. Одна колонка, шрифт Arial или Calibri 10–11 pt, поля 2 см, заголовки разделов — тот же шрифт, жирный, на 1–2 pt крупнее. Никаких таблиц, колонок, текстбоксов, иконок, фото, шкал навыков. Экспорт: DOCX (основной) и PDF (когда просят PDF). Имя файла: `Anton-Brilliantov-Senior-Backend-Engineer.pdf`.

Заголовки разделов оставлены ровно теми, которые распознаёт ATS: `SUMMARY`, `CORE COMPETENCIES`, `PROFESSIONAL EXPERIENCE`, `TECHNICAL SKILLS`, `OPEN SOURCE & PUBLICATIONS`, `CERTIFICATIONS`, `LANGUAGES`. Не переименовывать.

---

```
ANTON BRILLIANTOV
Senior Backend & Platform Engineer — Distributed Systems, Real-Time Data at Scale

Ramat Gan, Israel | brilliantov.anton@gmail.com | +972 55 772 0204
linkedin.com/in/anton-brilliantov-53152714b | github.com/brilliant-almazov


SUMMARY

Senior backend and platform engineer with 20 years in IT and over 10 years writing production
code in Go (Golang), Rust and PHP. Co-founder and CTO of an SEO analytics SaaS for eight years,
scaling it from 30,000 to over 1,300,000 daily queries per search engine and exiting in 2021.
Currently the platform architect of a Go and Rust microservices platform replacing a Symfony
monolith, with six bounded contexts delivered to production in six months. Deep experience in
distributed systems, event-driven architecture, high-load data pipelines, PostgreSQL and cloud
infrastructure on Google Cloud Platform. Seeking a senior backend, platform or software
architecture role.


CORE COMPETENCIES

Distributed Systems | Microservices Architecture | System Design | Software Architecture
Platform Engineering | Event-Driven Architecture | Message Queues (Kafka, RabbitMQ, NATS)
REST and gRPC API Design | Backend Development | Scalability and Performance Optimization
PostgreSQL, MySQL, Redis, BigQuery | Data Pipelines and ETL | SQL Optimization
CI/CD, Docker, Kubernetes, Google Cloud Platform | Observability and Monitoring
Technical Leadership | Code Review | Mentoring | Team Building


PROFESSIONAL EXPERIENCE

Senior Backend & Platform Engineer
Stealth Startup (Malta) — Marketing and SEO Analytics SaaS | Remote, Contract
Dec 2025 - Present

Sole platform architect on a two-engineer team, designing and delivering a Go and Rust
microservices platform that progressively replaces a domain-driven PHP and Symfony monolith.

- Designed and built a shared Go platform library imported by every microservice: resource
  lifecycle management, gRPC, HTTP, PostgreSQL, NATS, RabbitMQ and Redis clients, transactional
  outbox, Snowflake ID generation, structured logging, Prometheus metrics and an integration
  test harness. Reduced time to production for a new service from one week to one day.
- Extracted six bounded contexts from the monolith into production Go microservices, each
  deployed as several binaries (gRPC server, background worker, outbox and scheduler processes).
  Reduced resident memory from approximately 150 MB per Symfony daemon to 20 MB per Go binary
  and made every domain independently deployable and scalable.
- Developed a Rust sidecar replacing supervisord in PHP containers: a 3 MB static binary,
  drop-in compatible with existing configuration, approximately 17 times smaller than the
  runtime it replaced.
- Built a Go control-plane registry for cross-replica service discovery and a proxied
  administration API, using mutual Ed25519 authentication and push and pull heartbeats.
- Delivered the operational control plane: a Go backend-for-frontend and a React and TypeScript
  administration panel with role-based access control, audit logging, soft and hard delete and
  structured operational workflows, eliminating direct database access by operators.
- Established schema-first contracts in a shared Protocol Buffers repository as the single
  source of truth for all gRPC interfaces, generating client and server stubs for Go and PHP.
- Owned CI/CD across more than 20 repositories using GitHub Actions on self-hosted runners,
  with per-package test coverage gates and binary and image size budgets enforced on every
  pull request.
- Enforced a 90 percent test coverage floor in CI with integration tests running against real
  PostgreSQL, NATS and RabbitMQ instances rather than mocks.

Technologies: Go (Golang), Rust, PHP, Symfony, PostgreSQL, gRPC, Protocol Buffers, NATS,
RabbitMQ, Redis, BigQuery, React, TypeScript, Docker, Google Cloud Platform, GitHub Actions,
Prometheus, Grafana


Data Architect & BigQuery Consultant
Independent Consulting — Marketing Analytics and SaaS Backends | Part-time
Sep 2023 - Present

- Reduced a client's cloud costs by up to 10 times by redesigning the BigQuery SQL and data
  layer: table partitioning, clustering, materialized aggregates and elimination of full-scan
  queries.
- Reduced client onboarding time from 1-2 hours to 15 minutes by converting a manual launch
  checklist into an engineered, automated workflow.
- Designing a SaaS backend replacing no-code automation with explicit API contracts,
  idempotency, retry policies and observability.

Technologies: BigQuery, PostgreSQL, SQL, Google Cloud Platform, PHP, Symfony
References available on request.


Senior Backend Engineer / Team Lead
Lenvendo — Modular Ecommerce Engine (later spun out as SaaS)
Nov 2021 - Aug 2023 (1 year 10 months)

- Designed the modular core of the ecommerce engine using clean Symfony layering,
  domain-driven module boundaries and asynchronous messaging over Apache Kafka and RabbitMQ,
  allowing a new client vertical to be delivered as a module rather than a fork.
- Led a backend team of up to 6 engineers: code review, technical hiring, mentoring.
  Several junior engineers progressed to mid-level under my supervision.
- Worked directly with product management and clients on roadmap, technical specifications,
  demos and scope negotiation.

Technologies: PHP, Symfony, PostgreSQL, Redis, RabbitMQ, Apache Kafka, Kubernetes


Co-founder & Chief Technology Officer
Seowork — SEO Analytics SaaS | Successful exit 2021
Aug 2018 - Aug 2021 (3 years 1 month)

Technical co-founder of the spin-out that turned the search analytics platform into a
standalone SaaS, alongside the business founder, and CTO through to a successful exit in
2021. Eight years on the same product in total, from the first line of collection code in
2013 (Webit, then 404 Group) to the exit.

- Personally authored approximately 70 percent of the backend, in PHP and later Go (Golang)
  on high-throughput paths.
- Scaled query collection 40 times, from 30,000 to more than 1,300,000 queries per day per
  search engine, across Google, Yandex and others, with aggregate daily volume several times
  higher. Delivered without a rewrite, by evolving the data layer release by release with no
  service interruption.
- Designed and built the full downstream data pipeline: ingestion, deduplication,
  normalization, classification, scoring, materialized aggregates and retention policies.
- Delivered and retained enterprise clients including Ozon and M.Video, whose SEO teams based
  daily operational decisions on the platform's data.
- Grew the engineering team from 1 to 10 people (6-7 backend, 2-3 frontend, 1 QA), owning
  hiring, one-to-ones, architecture review and the on-call rotation.
- Owned product strategy jointly with the CEO: pricing, roadmap, release planning and
  database migration strategy.

Technologies: PHP, Go (Golang), MySQL, PostgreSQL, Redis, RabbitMQ


Head of Development
404 Group — Search Analytics Platform
Jul 2015 - Jul 2018 (3 years 1 month)

Ran development on the search analytics product as it moved from internal agency tooling to a
commercial platform with paying external clients.

- Owned the backend end to end: collection, storage, processing and reporting, including the
  decision on where the original design had to be replaced rather than patched as data volume
  grew.
- Built and led the engineering team: hiring, code review, architecture decisions and release
  process. These engineers became the founding SEOWORK team.
- Took the product from an internal utility to a commercial system external companies paid for
  and used for daily operational decisions, which made the 2018 spin-out possible.

Technologies: PHP, Go (Golang), MySQL, Redis, RabbitMQ


Backend Developer, Search Analytics and Internal Tooling
Webit — Full-Service Digital Agency
May 2013 - Jun 2015 (2 years 2 months)

Backend developer at a 100-person digital agency (founded 2003, later ranked first among SEO
agencies in the Ruward Award), working on the in-house tooling used by the agency's own SEO
department.

- Built the first version of the search-data collection backend: rank and visibility data
  across Google and Yandex, collected daily across the agency's client portfolio and served to
  analysts.
- Replaced manually assembled client reporting with generated reports, removing approximately
  one analyst-day per client per month.
- Served large ecommerce brands while still agency tooling, on a model billed on collected
  data and metered precisely, where an incorrect figure was an invoicing error rather than a
  cosmetic defect.
- Established cross-validation between data sources as standard practice before any figure
  reached a client report.
- This codebase became the origin of the SEO analytics product later spun out as SEOWORK.

Technologies: PHP, MySQL, Redis


Developer, Corporate Reporting & Internal Systems
NetByNet — National Internet Service Provider
Sep 2005 - Apr 2013 (8 years)

Eight years at one company across six roles. Joined a neighbourhood internet provider,
stayed through its acquisition by NetByNet, one of Russia's largest national providers, and
progressed into software development.

- Night-shift and day-shift telephone support, then field repairs at customer premises,
  then incident escalation and customer conflict resolution.
- Network engineering: network-level design and operations, then network engineer.
- One year in internal technical support, serving the company's own departments.
- Final eighteen months as a developer: built the corporate reporting the business made
  decisions on, covering IFRS and RAS financial reporting, revenue reporting and KPI
  tooling for department heads and the board.
- Developed custom call-centre software on Asterisk.

Technologies: SQL, PHP, Asterisk


TECHNICAL SKILLS

Programming Languages: Go (Golang), Rust, PHP, SQL, TypeScript, JavaScript
Frameworks: Symfony, React, Next.js
Databases: PostgreSQL, MySQL, Redis, BigQuery, database schema design, partitioning,
  query optimization, forward-only migrations
Messaging and Streaming: Apache Kafka, RabbitMQ, NATS JetStream, transactional outbox,
  at-least-once delivery
APIs and Contracts: gRPC, Protocol Buffers, REST, API design, backend-for-frontend
Cloud and Infrastructure: Google Cloud Platform (Cloud Run, Artifact Registry, BigQuery),
  Docker, Kubernetes, Terraform, Railway
DevOps and Quality: CI/CD, GitHub Actions, self-hosted runners, test-driven development,
  integration testing with Testcontainers, Prometheus, Grafana, structured logging,
  distributed tracing
Practices: distributed systems design, microservices, event-driven architecture,
  domain-driven design, monolith decomposition, technical leadership, mentoring, code review


OPEN SOURCE & PUBLICATIONS

Author, "Breaking the Monolith" — a 16-part technical series published on dev.to and LinkedIn
covering migration strategy, service boundary design, zero-downtime cutover, distributed
transactions, identity ownership and testing dual-write systems in production.

metrics-bridge-rs (Rust) — Prometheus exporter over Redis-backed PHP metrics storage.
Sub-millisecond response times compared to 50-200 ms through PHP; over 12,500 requests per
second with caching; verified against Redis, Dragonfly, Valkey and KeyDB.

pgenum (Go) — zero-dependency library for runtime management of PostgreSQL ENUM types through
the standard database/sql interface.

railway-exporter-rs (Rust) — Prometheus exporter for Railway.app billing and usage metrics.

github.com/brilliant-almazov


CERTIFICATIONS

Google Cloud — Modernizing Data Lakes and Data Warehouses with Google Cloud
Google Cloud — Building Resilient Streaming Analytics Systems on Google Cloud
Google Cloud — Modular Load Balancing with Terraform, Regional Load Balancer
Google Cloud — Getting Started with Google Kubernetes Engine
Google Cloud — Cloud SQL with Terraform


LANGUAGES

Russian — Native
English — Professional working proficiency
Hebrew — Elementary
```

---

## Что здесь сделано специально под ATS

| Приём | Зачем |
|---|---|
| `Go (Golang)` везде, где упоминается язык | Половина рекрутеров ищет `Golang`; по `Go` совпадения не будет |
| Стандартные заголовки капсом | `SUMMARY`, `PROFESSIONAL EXPERIENCE`, `TECHNICAL SKILLS` — их парсер знает; `What I bring` и `Career timeline` — нет |
| Порядок: должность → компания → даты | Самая распознаваемая последовательность полей |
| Длительность в скобках: `(8 years 3 months)` | Парсер и рекрутер получают стаж без счёта в уме |
| Запятые вместо `·` в перечислениях | `·` часть парсеров не считает разделителем и склеивает список в одну строку |
| Дефис `-` вместо `—` и `–` | Длинные тире изредка ломают кодировку при извлечении текста |
| Ни одной таблицы, иконки, эмодзи | Всё это либо игнорируется, либо рвёт текстовый поток |
| Ключевые слова внутри предложений, не списком | Современные ATS понижают ранг за очевидную набивку |
| `CORE COMPETENCIES` сразу после summary | Плотный блок ключевых слов в верхней трети — там, где рекрутер и скоринг смотрят первым делом |
| Телефон в международном формате | `+972 55 772 0204` распознаётся, `0557720204` — не всегда |

**Проверка перед отправкой:** открыть готовый PDF, выделить всё, вставить в блокнот. Если получившийся текст читается как связное резюме сверху вниз — ATS справится.
