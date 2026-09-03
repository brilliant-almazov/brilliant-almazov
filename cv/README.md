# Профиль и резюме — всё в одном файле

Копипаст сверху вниз. Думать не надо.
Остальные файлы в папке — разборы и обоснования; **для работы нужен только этот**.

---

# ЧАСТЬ 0. Что делать, по порядку

| # | Действие | Где взять текст | Время |
|---|---|---|---|
| 1 | LinkedIn: Headline, Location, Open to work | §1.1–1.3 | 5 мин |
| 2 | LinkedIn: Seowork — даты и должность ⚠️ главное | §1.8 | 5 мин |
| 3 | LinkedIn: удалить 404group, добавить NetByNet | §1.9–1.10 | 5 мин |
| 4 | LinkedIn: Analyzit → Part-time | §1.6 | 2 мин |
| 5 | LinkedIn: Featured — статьи первым элементом | §1.11 | 5 мин |
| 6 | LinkedIn: About | §1.4 | 3 мин |
| 7 | LinkedIn: Skills, порядок | §1.12 | 5 мин |
| 8 | LinkedIn: English → Professional working | §1.13 | 1 мин |
| 9 | Сверстать резюме для ATS-порталов | §2 | 30 мин |
| 10 | Резюме для отправки человеку | §3 | 15 мин |

Метрики — часть 4 и часть 7. Оценка «было → стало» — часть 8.

Пункты 1–5 дают больше всего. Это двадцать минут.

---

# ЧАСТЬ 1. LinkedIn — по блокам

**Лимиты LinkedIn.** Превышение — поле просто не сохраняется.

| Поле | Лимит | Наш текст |
|---|---:|---:|
| Headline | 220 | 172 |
| About | 2 600 | 2 382 |
| Experience, описание | 2 000 | Stealth 1 707 · Seowork 1 153 · остальные < 900 |
| Featured, описание | 300 | < 250 |

**Про формат.** LinkedIn не понимает markdown: ни `**жирного**`, ни `#`, ни `-` как буллета — всё превращается в кашу. Работают только пустые строки, юникод-символы (`▸ ━ ·`) и КАПС для подзаголовков. Текст сворачивается после третьей строки на «…see more» — первые две строки должны работать сами.

---

## 1.1 Headline

`Профиль → карандаш у имени → Headline`. Лимит 220 символов.

```
Senior Backend & Platform Engineer | Distributed Systems, Real-Time Data at Scale | Go · Rust · PHP · PostgreSQL | ex-CTO & co-founder (exit) | Writing "Breaking the Monolith"
```

## 1.2 Location

```
Ramat Gan, Israel
```

Сейчас стоит просто `Israel` — не попадаешь в гео-фильтры по Тель-Авивскому округу.

## 1.3 Open to work

`Кнопка «Open to» → Finding a new job`

- **Job titles:** `Senior Backend Engineer` · `Staff Backend Engineer` · `Platform Engineer` · `Backend Tech Lead` · `Software Architect` · `Data Platform Engineer`
- **Locations:** `Tel Aviv District, Israel` · `Israel (Remote)`
- **Job types:** Full-time, Contract
- **Start date:** Immediately
- **Visible to:** All LinkedIn members

## 1.4 About

`Раздел About → карандаш`. Вставить ровно так, вместе с пустыми строками и символами:

```
I build the systems other engineers build on — and I have run the product on top of them.

20 years in IT, 10+ writing production backends. Almost all of it the same shape of problem: data arriving faster than you would like, in volumes that punish sloppy design, in a system that has to stay correct while it grows.

━━━━━━━━━━━━━━━━━━

WHAT I HAVE BUILT

▸ Co-founder & CTO of an SEO analytics SaaS. 8 years, exited 2021.
Wrote ~70% of the backend. Scaled collection 40x, from 30,000 to 1,300,000+ queries per day per search engine, and built the pipeline underneath: ingestion, deduplication, normalisation, classification, scoring, aggregates, retention. Ozon and M.Video ran daily decisions on those numbers. Grew the team from myself to ten.

▸ Platform architect on a Go + Rust microservice platform, today.
Two-engineer AI-first team, progressively replacing a Symfony monolith. Six bounded contexts in production. A Go platform library every service imports, so a new service ships in a day instead of a week. Memory per worker down 7x. A Rust sidecar replacing supervisord at a seventeenth of its footprint. Metrics scrape latency from 50-200 ms to sub-millisecond.

▸ Data architecture, part-time.
A BigQuery redesign that cut a client's cloud bill by up to 10x and turned a two-hour onboarding into fifteen minutes.

━━━━━━━━━━━━━━━━━━

HOW I WORK

▸ 2,100+ production releases across 44 repositories, peaking at 31 per working day — each through the same 90% coverage gate and integration tests on real Postgres, NATS and RabbitMQ. Never mocks for infrastructure.
▸ Conventions codified per repository and enforced by tooling, so quality is mechanical rather than cultural.
▸ I have owned pricing, roadmap and the call about what not to build. I mentor, I review, and I will tell you plainly when a plan is wrong.

━━━━━━━━━━━━━━━━━━

I ALSO WRITE

"Breaking the Monolith" — 16 parts on dev.to, written from inside the process: migration strategy, service boundaries, zero-downtime cutover, and testing two systems that must agree while one replaces the other.

━━━━━━━━━━━━━━━━━━

WHAT I WANT NEXT

A platform or architecture role where the hard part is the system, not the ticket queue. Distributed services, real-time data, analytics. Industry matters far less than the shape of the problem.

Ramat Gan, Israel. On-site, hybrid or remote.
brilliantov.anton@gmail.com
```

## 1.5 Experience — текущее место

`Карандаш на записи Stealth Startup`

**Title:** `Senior Backend & Platform Engineer`
**Employment type:** `Contract` · **Location:** `Israel · Remote` · **Dates:** `Dec 2025 – Present`

```
Sole platform architect on a two-engineer, AI-first team. Building a Go + Rust microservice platform that progressively replaces a domain-driven Symfony monolith — for resource efficiency, not code quality.

▸ Built the Go platform library every service imports: resource lifecycle, gRPC/HTTP/Postgres/NATS/RabbitMQ/Redis wrappers, transactional outbox, Snowflake IDs, structured logging, Prometheus metrics, testcontainers harness. New service to production: one day instead of a week.

▸ Carved six bounded contexts out of the monolith into production Go services, each running several binaries (gRPC server, worker, outbox, scheduler). Resident memory down 7x, from 100+ MB per Symfony daemon to ~20 MB per Go binary; every domain independently deployable and scalable.

▸ Replaced supervisord with a ~3 MB Rust sidecar — drop-in for existing configs, ~17x smaller than the 50 MB runtime it removed.

▸ Cut Prometheus scrape latency 50-200x, from 50-200 ms through Symfony to sub-millisecond, sustaining 12,500+ RPS.

▸ Shipped a Go control-plane registry for cross-replica service discovery and a proxied admin API: single writer, mutual Ed25519 auth, push and pull heartbeat.

▸ Built the operational control plane — Go BFF plus React admin with RBAC, audit trail, soft-vs-hard delete. Operators never touch the database directly.

▸ Owned CI/CD across 20+ repositories: GitHub Actions on self-hosted runners, per-package coverage gates, binary and image size budgets on every PR. 90% coverage floor, integration tests on real Postgres/NATS/RabbitMQ, never mocks.

Go · Rust · PHP/Symfony · PostgreSQL · gRPC · NATS · RabbitMQ · Redis · BigQuery · React · TypeScript · Docker · GCP · Prometheus/Grafana
```

**Skills внутри записи:** `Go` · `Rust` · `Distributed Systems` · `Microservices` · `gRPC` · `PostgreSQL` · `Software Architecture` · `Platform Engineering`

## 1.6 Experience — консалтинг

`Карандаш на записи Analyzit`

**Title:** `Data Architect & BigQuery Consultant`
**Employment type:** ⚠️ `Part-time` · **Dates:** `Sep 2023 – Present`

```
A separate, part-time engagement alongside my main role — the data layer, where the money leaks.

▸ Cut a client's cloud bill by up to 10x by redesigning the BigQuery SQL and data layer: partitioning, clustering, materialised aggregates, and removing the full-scan queries that were quietly funding Google.

▸ Compressed client onboarding from 1-2 hours to 15 minutes by turning a manual launch checklist into an engineered workflow.

▸ Designing a SaaS backend that replaces Make/Zapier glue with explicit contracts, retries, idempotency and observability.

References available on request.

BigQuery · PostgreSQL · SQL · GCP
```

Без `Part-time` эта запись читается как второй фултайм параллельно текущему — первое, за что цепляется рекрутер.

## 1.7 Experience — Lenvendo

**Title:** `Senior Backend Engineer / Team Lead` · **Dates:** `Nov 2021 – Aug 2023`

```
Modular ecommerce engine, later spun out as a SaaS.

▸ Designed the modular core — clean Symfony layering, domain-driven module boundaries, async over Kafka and RabbitMQ — so a new client vertical is a module rather than a fork.

▸ Led a backend team of up to 6: code review, hiring filter, mentorship. Several juniors graduated into solid mids.

▸ Worked the product side directly with PM and client — roadmap, demos, specs and scope negotiation, including the unglamorous half: refusing features that would have made the engine unmaintainable.

PHP/Symfony · PostgreSQL · Redis · RabbitMQ · Kafka · Kubernetes
```

## 1.8 Experience — Seowork ⚠️ САМАЯ ВАЖНАЯ ПРАВКА

`Карандаш на записи SEOWORK.official`

Сейчас стоит **CTO, Aug 2018 – Aug 2021** — это выбрасывает пять лет и со-основательство.

**Title:** `Co-founder & CTO` · **Dates:** `Jun 2013` – `Aug 2021`

```
Built an SEO analytics SaaS from an empty repository into a load-bearing tool inside the largest Russian-speaking ecommerce companies. Exited in 2021 after eight years.

▸ Wrote ~70% of the backend personally — PHP first, then Go on the hot paths as volume outgrew the original design.

▸ Scaled query collection 40x, from 30,000 to 1,300,000+ per day per search engine. Google, Yandex and others each ran at that volume; aggregate collection was several times higher. No big-bang rewrite — the data layer evolved release by release while the product stayed up.

▸ Built the pipeline that consumed all of it: ingestion, deduplication, normalisation, classification, scoring, materialised aggregates, retention.

▸ Won and kept enterprise clients including Ozon and M.Video, whose SEO teams made daily calls on our data — which set the reliability bar for everything else.

▸ Grew the team from 1 to 10 (6-7 backend, 2-3 frontend, 1 QA), owning hiring, one-to-ones, architecture review and the on-call rotation.

▸ Owned the product, not just the stack — pricing, roadmap and release strategy with the CEO.

PHP · Go · MySQL/PostgreSQL · Redis · RabbitMQ
```

## 1.9 Experience — NetByNet (добавить)

`Experience → «+» → Add position`. Сейчас этого места в профиле нет — а это восемь лет.

**Title:** `Developer, Corporate Reporting & Internal Systems`
**Company:** `NetByNet` · **Dates:** `2005` – `Apr 2013`

```
Eight years at a national ISP, from the phone to the codebase — call-centre operator, field service, customer-facing and internal technical support, then development.

As a developer I built the corporate reporting systems the company's business analysts ran on: IFRS and RAS financial reporting, KPI tooling, and custom call-centre software on Asterisk.

Where I learned that the database is the soul of the product, and that most operational pain is a bad query wearing a costume.
```

Коротко намеренно: это 2005–2013, детали уже никого не интересуют. Ценность — восемь лет стажа, рост от телефона до разработчика, и аналитика с данными с самого начала карьеры.

## 1.10 Experience — 404group: удалить

`Карандаш → Delete position`. Это была часть истории Seowork, а не отдельное место; сейчас висит четырьмя годами внахлёст и читается как небрежность в датах.

## 1.11 Featured — сюда идут статьи

`Featured → «+» → Add a link`. Три элемента, в этом порядке:

**1. Серия статей** — самый недооценённый актив профиля.
- Link: ссылка на профиль dev.to / на серию
- Title: `Breaking the Monolith — a 16-part engineering series`
- Description: `Splitting a live PHP monolith into Go microservices, written from inside the process: cutover without a flag day, identity ownership, sagas, gateways, Snowflake IDs, platform runtime.`

**2. Архитектура**
- Link: `https://github.com/brilliant-almazov/brilliant-almazov`
- Title: `Platform architecture — full technical breakdown`
- Description: `Distributed system map, platform library design, migration strategy, quality standards.`

**3. Open source**
- Link: `https://github.com/brilliant-almazov/metrics-bridge-rs`
- Title: `metrics-bridge-rs — Rust Prometheus exporter`
- Description: `Sub-millisecond responses against 50-200 ms through PHP. 12,500+ RPS with caching, verified across Redis, Dragonfly, Valkey and KeyDB.`

**Зачем.** Резюме пишут все; шестнадцать технических статей — нет. Инженерный менеджер видит, что ты умеешь формулировать решение, а не только принимать его; рекрутер видит неподделываемый сигнал seniority; команда получает ответ на «а как он объясняет сложное» — ровно ту компетенцию, которую ждут от tech lead. Отдельно про Израиль: рынок маленький и networked, публичный технический след здесь работает сильнее, чем в большом рынке — тебя находят по статье, а не по отклику.

**В привычку:** каждую новую часть постить отдельным постом в LinkedIn, 3–4 абзаца плюс ссылка. Это единственный способ, которым профиль работает сам, пока ты занят кодом.

## 1.12 Skills — порядок важен

**Top 3 (закрепить, они в превью):**
```
Distributed Systems
Software Architecture
Go (Programming Language)
```

**Дальше:**
```
Platform Engineering · Microservices · PostgreSQL · gRPC · Rust · Event-Driven Architecture ·
Message Queues (RabbitMQ, NATS, Kafka) · BigQuery · Data Pipelines · Scalability · System Design ·
Technical Writing · PHP · Symfony · Redis · Docker · Kubernetes · Google Cloud Platform · CI/CD ·
Observability (Prometheus, Grafana) · Technical Leadership · Mentoring
```

Сейчас в топе `Rust`, `Go`, `Distributed Systems`. Первыми должны стоять роль и область, а не язык.

## 1.13 Languages

- `Russian` → **Native or bilingual**
- `English` → **Professional working** ← поменять с `Limited working`
- `Hebrew` → **Elementary**

`Limited working` — стоп-сигнал до разговора. `Professional working` соответствует реальности: читаешь, пишешь, ревьюишь и публикуешь технические статьи на английском.

## 1.14 Что убрать

- `3.4M LOC` и `6,300 commits` из headline и About. Метрика не врёт, но у неё свой читатель: в GitHub-профиле она стоит рядом с coverage floor и real-infra тестами — там видно, что объём не стал долгом. В LinkedIn этого контекста нет, и она читается наоборот.
- Ссылку на чужой LinkedIn из описания Analyzit — заменена на `References available on request`.
- Шесть из семи ссылок на GitHub в контактах — остальное живёт в Featured.
- `Gaming Vertical` из названия текущего места. Компанию не палим, индустрии в описании достаточно.

---

# ЧАСТЬ 2. Резюме для ATS-порталов

Для откликов через Greenhouse, Lever, Comeet, Workday.

## 2.1 Почему текущий файл не проходит

`Profile (3).pdf` — экспорт LinkedIn: **две колонки и тёмный сайдбар**. Парсер читает построчно слева направо и склеивает колонки в один поток. В сайдбаре при этом лежат контакты, Top Skills, языки и сертификаты — именно это теряется.

**Одна колонка. Всегда. Никаких сайдбаров.**

## 2.2 Правила вёрстки

| Правило | Почему |
|---|---|
| Одна колонка, без таблиц, текстбоксов, колонтитулов | Многоколоночная вёрстка парсится в мусор |
| Контакты обычным текстом вверху **тела**, не в header страницы | Header/footer многие парсеры не читают |
| DOCX для подачи, PDF когда просят PDF | DOCX парсится точнее |
| Заголовки строго: `SUMMARY`, `PROFESSIONAL EXPERIENCE`, `TECHNICAL SKILLS`, `CERTIFICATIONS`, `LANGUAGES` | Парсер ищет буквально эти слова |
| Порядок: должность → компания → даты | Самая распознаваемая последовательность |
| Даты единообразно: `Jun 2013 - Aug 2021` | Разнобой ломает вычисление стажа |
| Запятые вместо `·`, дефис вместо `—` | `·` не считается разделителем; длинные тире ломают кодировку |
| `Go (Golang)` везде | Половина рекрутеров ищет `Golang`; по `Go` совпадения не будет |
| Никаких иконок, эмодзи, шкал навыков, фото | Ломают текстовый поток |
| Шрифт Arial или Calibri 10–11 pt | Экзотика извлекается с битой кодировкой |
| Имя файла `Anton-Brilliantov-Senior-Backend-Engineer.pdf` | Попадает в карточку кандидата |

**Проверка:** открыть готовый PDF, выделить всё, вставить в блокнот. Читается связно сверху вниз — ATS справится.

## 2.3 Текст резюме под ATS

```
ANTON BRILLIANTOV
Senior Backend & Platform Engineer - Distributed Systems, Real-Time Data at Scale

Ramat Gan, Israel | brilliantov.anton@gmail.com | +972 55 772 0204
linkedin.com/in/anton-brilliantov-53152714b | github.com/brilliant-almazov


SUMMARY

Senior backend and platform engineer with 20 years in IT and over 10 years writing production
code in Go (Golang), Rust and PHP. Co-founder and CTO of an SEO analytics SaaS for eight years,
scaling it 40 times from 30,000 to over 1,300,000 daily queries per search engine and exiting
in 2021. Currently the platform architect of a Go and Rust microservices platform replacing a
Symfony monolith, with six bounded contexts delivered to production in six months and a 7x
reduction in per-worker memory. Deep experience in distributed systems, event-driven
architecture, high-load data pipelines, PostgreSQL and cloud infrastructure on Google Cloud
Platform. Seeking a senior backend, platform or software architecture role.


CORE COMPETENCIES

Distributed Systems | Microservices Architecture | System Design | Software Architecture
Platform Engineering | Event-Driven Architecture | Message Queues (Kafka, RabbitMQ, NATS)
REST and gRPC API Design | Backend Development | Scalability and Performance Optimization
PostgreSQL, MySQL, Redis, BigQuery | Data Pipelines and ETL | SQL Optimization
CI/CD, Docker, Kubernetes, Google Cloud Platform | Observability and Monitoring
Technical Leadership | Code Review | Mentoring | Team Building


PROFESSIONAL EXPERIENCE

Senior Backend & Platform Engineer
Stealth Startup (Malta) - Marketing and SEO Analytics SaaS | Remote, Contract
Dec 2025 - Present

Sole platform architect on a two-engineer team, designing and delivering a Go and Rust
microservices platform that progressively replaces a domain-driven PHP and Symfony monolith.

- Designed and built a shared Go platform library imported by every microservice: resource
  lifecycle management, gRPC, HTTP, PostgreSQL, NATS, RabbitMQ and Redis clients, transactional
  outbox, Snowflake ID generation, structured logging, Prometheus metrics and an integration
  test harness. Reduced time to production for a new service from one week to one day.
- Extracted six bounded contexts from the monolith into production Go microservices, each
  deployed as several binaries (gRPC server, background worker, outbox and scheduler processes).
  Reduced resident memory approximately 7 times, from over 100 MB per Symfony daemon to 20 MB
  per Go binary, and made every domain independently deployable and scalable.
- Developed a Rust sidecar replacing supervisord in PHP containers: a 3 MB static binary,
  drop-in compatible with existing configuration, approximately 17 times smaller than the
  50 MB runtime it replaced.
- Reduced Prometheus scrape latency by 50 to 200 times, from 50-200 ms through Symfony to
  sub-millisecond, sustaining over 12,500 requests per second with caching.
- Built a Go control-plane registry for cross-replica service discovery and a proxied
  administration API, using mutual Ed25519 authentication and push and pull heartbeats.
- Delivered the operational control plane: a Go backend-for-frontend and a React and TypeScript
  administration panel with role-based access control, audit logging, soft and hard delete and
  structured operational workflows, eliminating direct database access by operators.
- Established schema-first contracts in a shared Protocol Buffers repository as the single
  source of truth for all gRPC interfaces, generating stubs for Go and PHP.
- Owned CI/CD across more than 20 repositories using GitHub Actions on self-hosted runners,
  with per-package test coverage gates and binary and image size budgets enforced on every
  pull request.
- Enforced a 90 percent test coverage floor in CI with integration tests running against real
  PostgreSQL, NATS and RabbitMQ instances rather than mocks.

Technologies: Go (Golang), Rust, PHP, Symfony, PostgreSQL, gRPC, Protocol Buffers, NATS,
RabbitMQ, Redis, BigQuery, React, TypeScript, Docker, Google Cloud Platform, GitHub Actions,
Prometheus, Grafana


Data Architect & BigQuery Consultant
Independent Consulting - Marketing Analytics and SaaS Backends | Part-time
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
Lenvendo - Modular Ecommerce Engine (later spun out as SaaS)
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
Seowork - SEO Analytics SaaS | Exited 2021
Jun 2013 - Aug 2021 (8 years 3 months)

Built an SEO analytics SaaS platform from zero into a production system used daily by the
largest Russian-speaking ecommerce companies. Exited the company in 2021.

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


Developer, Corporate Reporting & Internal Systems
NetByNet - National Internet Service Provider
2005 - Apr 2013 (8 years)

Progressed over eight years from call-centre operator and field service technician through
customer-facing and internal technical support into software development.

- Built the corporate financial reporting systems used by the company's business analysts,
  covering IFRS and RAS reporting and KPI tooling.
- Developed custom call-centre software on Asterisk.

Technologies: SQL, PHP, Asterisk


TECHNICAL SKILLS

Programming Languages: Go (Golang), Rust, PHP, SQL, TypeScript, JavaScript
Frameworks: Symfony, React, Next.js
Databases: PostgreSQL, MySQL, Redis, BigQuery, schema design, partitioning, query
  optimization, forward-only migrations
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

Author, "Breaking the Monolith" - a 16-part technical series published on dev.to and LinkedIn
covering migration strategy, service boundary design, zero-downtime cutover, distributed
transactions, identity ownership and testing dual-write systems in production.

metrics-bridge-rs (Rust) - Prometheus exporter over Redis-backed PHP metrics storage.
Sub-millisecond response times compared to 50-200 ms through PHP; over 12,500 requests per
second with caching; verified against Redis, Dragonfly, Valkey and KeyDB.

pgenum (Go) - zero-dependency library for runtime management of PostgreSQL ENUM types through
the standard database/sql interface.

railway-exporter-rs (Rust) - Prometheus exporter for Railway.app billing and usage metrics.

github.com/brilliant-almazov


CERTIFICATIONS

Google Cloud - Modernizing Data Lakes and Data Warehouses with Google Cloud
Google Cloud - Building Resilient Streaming Analytics Systems on Google Cloud
Google Cloud - Modular Load Balancing with Terraform, Regional Load Balancer
Google Cloud - Getting Started with Google Kubernetes Engine
Google Cloud - Cloud SQL with Terraform


LANGUAGES

Russian - Native
English - Professional working proficiency
Hebrew - Elementary
```

## 2.4 Под конкретную вакансию

Открыть описание, выписать 10–15 повторяющихся терминов, убедиться, что каждый встречается в резюме **внутри осмысленной фразы**. Не списком в конце: современные ATS понижают ранг за очевидную набивку ключевых слов.

---

# ЧАСТЬ 3. Резюме для человека

Когда резюме идёт напрямую hiring manager'у по почте или в мессенджер — берётся текст из §2.3, но можно вернуть форматирование: жирный на цифрах, таблицу метрик из §4.1 сразу после summary, ссылки живыми. Полная версия с оформлением — файл `02-CV-optimized.md`.

Разница одна: ATS-версия оптимизирована под парсер, человеческая — под глаз. Факты и цифры одинаковые.

---

# ЧАСТЬ 4. Метрики

Единый справочник. На интервью и в письмах брать отсюда, чтобы цифры не расходились.

## 4.1 Производительность и ресурсы — текущая платформа

| Что | До (PHP) | После (Go / Rust) | Выигрыш |
|---|---|---|---|
| Резидентная память на воркер | 100+ MB, Symfony-демон ~150 MB | **~20 MB** на Go-бинарь | **~7×** |
| Размер образа контейнера | 100+ MB | **~20–30 MB** (Go на alpine) | **5–10×** |
| Отпечаток менеджера процессов | ~50 MB Python supervisord | **~3 MB** Rust sidecar | **~17×** |
| Латентность Prometheus-скрейпа | 50–200 ms через Symfony | **суб-миллисекунда** через Rust-мост | **50–200×** |
| Пропускная способность экспортера | — | **12,500+ RPS** с кэшем | — |
| Время до продакшена нового сервиса | ~неделя | **1 день** | **~5×** |

**Как формулировать:** «Это не синтетика. Одна и та же продовая нагрузка, замеренная до и после каждого отделения сервиса. Каждый шаг виден в Grafana, и мы не двигались дальше, пока метрики не показывали, что новый путь здоров».

**Оговорка, которая работает сильнее самой цифры:** «10× — это не „та же нагрузка теперь ест в десять раз меньше RAM“. Это „бюджет на следующий десятикратный рост продукта помещается в текущий контур инфраструктуры“».

## 4.2 Деньги и время — консалтинг

| Что | До | После | Выигрыш |
|---|---|---|---|
| Счёт за облако (BigQuery) | baseline | **до 10× меньше** | **10×** |
| Онбординг клиента | 1–2 часа | **15 минут** | **4–8×** |

Как достигнуто: партиционирование, кластеризация, материализованные агрегаты, устранение full-scan запросов; ручной чек-лист заменён инженерным workflow.

## 4.3 Масштаб — Seowork

| Метрика | Значение |
|---|---|
| Сбор запросов, старт → выход | 30,000 → **1,300,000+ в сутки на поисковую систему** (**40×**) |
| Совокупный объём | в несколько раз выше, суммарно по Google, Yandex и другим |
| Доля бэкенда лично | **~70%** |
| Команда | **с 1 до 10** (6–7 backend, 2–3 frontend, 1 QA) |
| Длительность / исход | **8 лет** · **экзит 2021** |
| Клиенты | Ozon, M.Video |

## 4.4 Объём и дисциплина — текущая работа

| Метрика | Значение |
|---|---|
| Bounded contexts в проде | **6** (каждый — несколько бинарей) |
| Активных репозиториев / под единым CI | **22** / **20+** |
| Порог покрытия в CI | **90%** |
| Публичных OSS-библиотек | **3** |
| Опубликованных статей | **16** |
| Коммитов за 6 месяцев | 6,300+ (~32/день) |
| Строк исходного кода за 6 месяцев | 3.4M |

⚠️ Две последние строки — **только для инженерного читателя и только с контекстом**. В резюме и LinkedIn их нет: без объяснения дисциплины они читаются как «AI навалил кода».

**Если спросят на интервью:** «Скорость обеспечена AI. Качество — дисциплиной, которая механическая, а не культурная: конвенции закодированы по репозиториям и проверяются хуками, порог покрытия стоит в CI, интеграционные тесты гоняются на настоящих Postgres, NATS и RabbitMQ, а не на моках. Архитектурные решения проходят через меня. Модель хороша в исполнении и плоха в суждении».

## 4.5 Стаж

| Метрика | Значение |
|---|---|
| Всего в IT | **20 лет** |
| Production-код | **10+ лет** |
| PHP / Symfony | **15+ лет** |
| Дыр в датах | нет, 2005 → настоящее время |
| Самое долгое место | 8 лет, дважды (NetByNet, Seowork) |

## 4.6 Распределение по языкам (Dec 2025 → Jun 2026, все репозитории)

PHP ~55% · Go ~30% · TypeScript/React ~8% · SQL/Proto/YAML ~4% · Rust ~3%

Полезно, когда спрашивают «а Go у вас правда основной или для галочки».

## 4.7 Куда какая цифра идёт

| Поверхность | Что берём |
|---|---|
| Headline, первые две строки | 30K → 1.3M, экзит, 6 контекстов за 6 месяцев |
| Summary резюме | 20 лет, 10+ прод, 40×, экзит 2021, 7× память |
| Опыт | всё из §4.1–4.3, привязанное к местам |
| LinkedIn About | 40×, 10× облако, 17× sidecar, 7× память, 90% покрытие, 16 статей |
| Сопроводительное письмо | одна-две цифры, релевантные вакансии |
| Интервью | всё, включая §4.4 с объяснением |
| Без контекста не публиковать | 3.4M LOC, 6,300 коммитов |

## 4.8 Чего пока нет и стоит замерить

Первые три спрашивают на интервью почти всегда:

- **p99 латентность** ключевых gRPC-ручек, до и после отделения сервиса
- **RPS / QPS** внешнего гейтвея на пике
- **Uptime / SLA** за период
- MTTR по инцидентам, до и после введения наблюдаемости
- Стоимость инфраструктуры в месяц, в деньгах, а не в разах
- Объём данных: строк, терабайт
- Скорость доставки: релизов в неделю, lead time от коммита до прода

---

# ЧАСТЬ 5. Что чинится и почему

Коротко, чтобы понимать логику правок и дальше держать её самому.

## 5.1 Главная проблема была не в опыте

Опыт закрывает staff-уровень: 20 лет без дыр, со-основатель и CTO с экзитом, 40× рост под нагрузкой, enterprise-клиенты, три языка в проде, платформенный слой целиком, команда с 1 до 10, три OSS-библиотеки, 16 статей, 10× экономии в деньгах. Упаковка отдавала это за мидла: сильные факты лежали на третьей странице, слабые — в заголовке.

## 5.2 Что резало глаз в старой версии

| Что | Почему плохо |
|---|---|
| Заголовок-абзац с `3.4M LOC` и `6,300 commits` | Должность не считывается; LOC для инженерного читателя — анти-метрика |
| `English (Limited Working)` | Самодисквалификация до собеседования |
| Нахлёст дат (Analyzit ∥ Stealth, 404group ∥ Seowork) | Читается как небрежность или фриланс, выданный за фултайм |
| Seowork как «CTO, 3 года» | Выброшено пять лет, со-основательство и экзит |
| Продуктового опыта нет вовсе | Инженеров с Go много; с экзитом — мало. Отличие было потеряно |
| Analyzit: 3 года, 4 строки, ссылка на чужой LinkedIn | Место потрачено зря |
| Ни одной операционной цифры | Нечем зацепиться за 8 секунд |
| Двухколоночный PDF с тёмным сайдбаром | ATS склеивает колонки и теряет контакты со скиллами |

## 5.3 Формула пункта опыта

**Глагол → что построил → масштаб → что изменилось.**

Было: «Developed a systematic approach to SQL and data layers in BigQuery, optimizing performance.»
Стало: «Cut a client's cloud bill by up to 10× by redesigning the BigQuery SQL and data layer: partitioning, clustering, materialised aggregates, and killing the full-scan queries that were quietly funding Google.»

Результат впереди, метод следом, конкретика вместо «systematic approach».

## 5.4 Три поверхности, один таймлайн

| Документ | Читатель |
|---|---|
| ATS-версия (§2.3) | парсер, потом рекрутер |
| Человеческая версия (`02-CV-optimized.md`) | hiring manager |
| GitHub-профиль (`03-github-profile-optimized.md`) | инженер, тимлид, CTO |
| LinkedIn (§1) | и те и другие |

Один таймлайн, один набор цифр везде. Расхождение между ними — единственное, что гарантированно стоит собеседования.

---

# ЧАСТЬ 6. Канонический таймлайн

Подтверждён владельцем. Идёт во все поверхности без изменений.

| Период | Место | Роль |
|---|---|---|
| 2005 – Apr 2013 | NetByNet | Developer, corporate reporting & internal systems · 8 лет |
| Jun 2013 – Aug 2021 | Seowork | **Co-founder & CTO · 8 лет · экзит 2021** |
| Nov 2021 – Aug 2023 | Lenvendo | Senior backend engineer / team lead |
| Sep 2023 – present | Independent consulting | Data architect & BigQuery · **part-time** |
| Dec 2025 – present | Stealth startup (Malta) | Senior backend & platform engineer · contract |

**404group** — часть истории Seowork, а не отдельное место. В резюме не идёт, из LinkedIn удаляется.

**NetByNet** — восемь лет в одной компании, рост снизу: оператор колл-центра, выезды на ремонты, клиентская и внутренняя техподдержка, затем разработка. Как разработчик — системы корпоративной отчётности для бизнес-аналитиков: МСФО и РСБУ, KPI-инструменты, софт колл-центра на Asterisk. В резюме коротко: важны стаж, рост и то, что аналитика с данными были с начала карьеры.

**Independent consulting** — помощь Натану Крейдерману: данные, BigQuery, SQL-слой, стоимость облака. Рекомендации есть, в тексте стоит `References available on request`.

---

# ЧАСТЬ 7. Скорость доставки — замеренная

Самая недооценённая метрика профиля. Её никто не пишет в резюме, а именно её ищут платформенные команды: «как быстро у вас код доходит до прода и не ломает ли это качество».

Цифры сняты по git-истории 44 репозиториев: теги = релизы в прод.

## 7.1 Релизы

| Метрика | Значение |
|---|---|
| Всего релизных тегов | **2,112** |
| Всего коммитов | **~15,100** |
| Активных репозиториев | **44** (из них 22 в текущей платформе) |
| Пиковый месяц (июль 2026) | **696 релизов** ≈ **31 релиз в рабочий день** |
| Средний темп, Mar–Aug 2026 | **~346 релизов в месяц** ≈ **16 в рабочий день** |

## 7.2 По ключевым сервисам

| Сервис | Коммитов | Релизов | Период | Темп |
|---|---:|---:|---|---|
| cgw-admin | 1,184 | 385 | 12.5 мес | ~31 релиз/мес |
| cgw-backend (монолит) | 4,100 | 339 | 3 года | ~9 релизов/мес |
| provider-sender | 1,878 | 245 | 5 мес | ~49 релизов/мес |
| cgw-backend-go | 809 | 204 | 3.5 мес | ~58 релизов/мес |
| cgw-gateway | 954 | 191 | 1.5 мес | **~127 релизов/мес** |
| cgw-drm | 800 | 161 | 2.4 мес | ~67 релизов/мес |
| cgw-proto (контракты) | 582 | 74 | 4 мес | ~18 релизов/мес |
| cgw-platform (библиотека) | 742 | 34 | 4 мес | ~8 релизов/мес |

## 7.3 Как это подавать

**В резюме, строкой в блоке текущего места:**

```
- Sustained a release cadence of 15-30 production releases per working day across 20+
  services, with a 90 percent coverage floor and integration tests against real
  infrastructure gating every one of them.
```

**В LinkedIn About, в блок HOW I WORK:**

```
▸ 2,100+ production releases across 44 repositories, peaking at 31 releases per working day — every one of them through the same coverage gate and real-infrastructure integration tests.
```

**На интервью:** «Скорость доставки — не следствие того, что мы срезаем углы, а следствие того, что срезать углы физически нельзя: конвенции проверяются хуками, покрытие стоит порогом в CI, интеграционные тесты гоняются на настоящих Postgres, NATS и RabbitMQ. Релиз проходит через те же ворота, что и любой другой. Поэтому 30 релизов в день — это безопасно».

**Почему это работает лучше, чем «6,300 коммитов».** Коммит — это активность. Релиз — это доставленная в прод ценность, прошедшая через ворота качества. Первое рекрутер читает как объём, второе — как зрелость инженерной практики. При этом обе цифры про одно и то же, просто вторая измеряет результат, а не усилие.

**Что усилит ещё, если замерить:** lead time от коммита до прода, доля откатов (change failure rate), MTTR. Это классическая четвёрка DORA, и по трём метрикам из четырёх у тебя уже сильные значения — не хватает только честного замера.

---

# ЧАСТЬ 8. Индекс привлекательности профиля

Как измерить «было → стало». Десять критериев, по которым профиль реально отсеивают, каждый по 10 баллов, с весом.

## 8.1 Шкала

| # | Критерий | Вес | Что оценивается |
|---|---|---:|---|
| 1 | ATS-проходимость | 15% | Парсится ли файл: колонки, заголовки, поля, формат дат |
| 2 | Совпадение по ключевым словам | 15% | Есть ли термины вакансии внутри осмысленных фраз |
| 3 | Считываемость роли за 8 секунд | 10% | Понятно ли из верхней трети, кто ты и на что претендуешь |
| 4 | Плотность измеримых результатов | 15% | Сколько цифр «до → после» на документ |
| 5 | Сигналы seniority и масштаба | 10% | Экзит, размер команды, объём нагрузки, владение платформой |
| 6 | Консистентность поверхностей | 10% | Совпадают ли резюме, LinkedIn и GitHub |
| 7 | Отсутствие красных флагов | 10% | Нахлёсты дат, дыры, самодисквалификация по языку |
| 8 | Продуктовый и лидерский трек | 5% | Владение продуктом, наём, менторство |
| 9 | Публичный технический след | 5% | OSS, статьи, выступления |
| 10 | Гео и логистика | 5% | Город, готовность к формату работы |

## 8.2 Оценка: было → стало

| # | Критерий | Было | Стало | Что изменилось |
|---|---|---:|---:|---|
| 1 | ATS-проходимость | **2** | **9** | Было: две колонки с тёмным сайдбаром, контакты и скиллы теряются при парсинге. Стало: одна колонка, стандартные заголовки, `Go (Golang)`, запятые вместо `·` |
| 2 | Ключевые слова | **4** | **9** | Добавлены `Distributed Systems`, `System Design`, `Scalability`, `Event-Driven Architecture`, `Data Pipelines`, `ETL`, `Golang`, `Observability` — внутри фраз, не списком |
| 3 | Считываемость за 8 сек | **2** | **9** | Было: заголовок-абзац с LOC и коммитами. Стало: должность одной строкой + экзит + масштаб в первых трёх строках |
| 4 | Измеримые результаты | **3** | **10** | Было 2 цифры (1.3M, 10×). Стало 15+: 7× память, 17× sidecar, 50–200× латентность, 40× рост, 5–10× образ, 4–8× онбординг, 2,112 релизов, 90% покрытие |
| 5 | Сигналы seniority | **5** | **9** | Seowork поднят с «CTO, 3 года» до «Co-founder & CTO, 8 лет, экзит»; команда 1→10; платформенный слой целиком |
| 6 | Консистентность | **2** | **9*** | Было: LinkedIn и GitHub описывают разные карьеры. Стало: один таймлайн везде — **при условии, что LinkedIn правится по части 1** |
| 7 | Красные флаги | **3** | **9** | Убраны нахлёсты дат, `404group`, `English (Limited Working)`, ссылка на чужой профиль |
| 8 | Продукт и лидерство | **2** | **9** | Было: не упомянуто вовсе. Стало: pricing, roadmap, «что не строить», наём, менторство, свой SaaS |
| 9 | Публичный след | **3** | **9** | Было: OSS упомянут вскользь, статей нет. Стало: 16 статей серией + 3 OSS в Featured |
| 10 | Гео и логистика | **4** | **9** | `Israel` → `Ramat Gan, Israel`, добавлен формат работы и Open to work с шестью тайтлами |

## 8.3 Итог

```
Было:   2×0.15 + 4×0.15 + 2×0.10 + 3×0.15 + 5×0.10 + 2×0.10 + 3×0.10 + 2×0.05 + 3×0.05 + 4×0.05
      = 0.30 + 0.60 + 0.20 + 0.45 + 0.50 + 0.20 + 0.30 + 0.10 + 0.15 + 0.20
      = 3.0 / 10

Стало:  9×0.15 + 9×0.15 + 9×0.10 + 10×0.15 + 9×0.10 + 9×0.10 + 9×0.10 + 9×0.05 + 9×0.05 + 9×0.05
      = 1.35 + 1.35 + 0.90 + 1.50 + 0.90 + 0.90 + 0.90 + 0.45 + 0.45 + 0.45
      = 9.15 / 10
```

**3.0 → 9.2**

Важно понимать, что именно выросло: **не опыт, а его читаемость**. Все факты в правой колонке были и раньше — они лежали на третьей странице, в сайдбаре, который не парсится, или не были написаны вовсе. Профиль на 3.0 отдавал staff-уровневый опыт за мидла.

## 8.4 Что осталось не закрытым

| Критерий | Почему не 10 |
|---|---|
| Консистентность (6) | Балл станет реальным только после правки LinkedIn по части 1. До этого — 2 |
| Измеримые результаты (4) | Нет p99, RPS на пике, uptime, MTTR, стоимости инфраструктуры в деньгах. См. §4.8 |
| Ключевые слова (2) | Под каждую вакансию нужен свой прогон: выписать 10–15 терминов из описания и проверить наличие |
| Публичный след (9) | Вырастет, если каждая новая статья идёт отдельным постом в LinkedIn |

## 8.5 Как перемерить потом

Пройти по таблице 8.2, выставить баллы честно, посчитать по формуле 8.3. Делать после каждой существенной правки профиля — раз в квартал или после серии отказов. Если балл высокий, а откликов нет — проблема не в резюме, а в таргетинге вакансий, и чинится она в другом месте.

---

## Остальные файлы папки

Разборы и обоснования — открывать, только если нужно понять, почему что-то сформулировано именно так.

| Файл | Что внутри |
|---|---|
| `01-разбор-текущего-резюме.md` | Полный разбор старой версии глазами HR |
| `02-CV-optimized.md` | Человеческая версия резюме с оформлением |
| `03-github-profile-optimized.md` | Готовый README для GitHub-профиля |
| `04-как-это-переписано.md` | Правила трансформации формулировок |
| `05-linkedin-по-блокам.md` | Развёрнутая версия части 1 |
| `06-ats-и-hr-ревью.md` | Развёрнутая версия части 2 |
| `07-CV-ats-safe.md` | Развёрнутая версия §2.3 |
| `08-метрики.md` | Развёрнутая версия части 4 |
