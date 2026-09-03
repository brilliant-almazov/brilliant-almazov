# LinkedIn — по блокам. Копипаст, думать не надо

**Цель позиционирования:** platform / distributed systems, реалтайм и данные под нагрузкой, дорога в tech lead / architect.
**Индустрия не важна.** Важно: аналитика, статистика, поток данных, распределённые системы.

Порядок — сверху вниз по странице профиля. Каждый блок: *куда жать* → *что вставить*.

---

## 1. Headline (под именем)

`Меня → Открыть профиль → карандаш у имени → поле «Headline»`

Лимит 220 символов. Вставить:

```
Senior Backend & Platform Engineer | Distributed Systems, Real-Time Data at Scale | Go · Rust · PHP · PostgreSQL | ex-CTO & co-founder (exit) | Writing "Breaking the Monolith"
```

**Почему так.** Первое — роль, которую ищешь. Второе — область (это то, что рекрутер матчит). Третье — стек для ATS. Четвёртое — экзит: отделяет от сотни таких же сеньоров. Пятое — серия статей: показывает, что ты не просто делаешь, а формулируешь. Никаких LOC и коммитов: здесь у них нет контекста, и читается это как объём, а не как качество.

---

## 2. Location

`Тот же экран → Location`

```
Ramat Gan, Israel
```

Сейчас стоит просто `Israel`. Город даёт попадание в геофильтры рекрутеров по Тель-Авивскому округу.

---

## 3. Open to work

`Кнопка «Open to» → Finding a new job`

- **Job titles:** `Senior Backend Engineer` · `Staff Backend Engineer` · `Platform Engineer` · `Backend Tech Lead` · `Software Architect` · `Data Platform Engineer`
- **Locations:** `Tel Aviv District, Israel` · `Israel (Remote)`
- **Job types:** Full-time, Contract
- **Start date:** Immediately
- **Visible to:** All LinkedIn members

Названия должностей — это буквально то, по чему ищет рекрутер. `Software Architect` и `Backend Tech Lead` добавлены осознанно: это дорога, в которую ты идёшь.

---

## 4. About ⚠️ переформатировано под LinkedIn

`Раздел About → карандаш`

**Важно про формат.** LinkedIn не понимает markdown: ни `**жирного**`, ни `#`, ни `-` как буллета. Всё превращается в кашу. Работают только: пустые строки, юникод-символы (`▸ ━ ·`) и КАПС для подзаголовков. Плюс LinkedIn сворачивает текст после третьей строки на «…see more» — поэтому первые две строки должны работать сами по себе.

Вставить ровно так, вместе с пустыми строками и символами:

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

---

## 5. Experience — блок 1: текущий

`Experience → карандаш на записи Stealth Startup`

**Title:**
```
Senior Backend & Platform Engineer
```

**Company:** оставить `Stealth Startup (Malta)`
**Employment type:** `Contract`
**Location:** `Israel · Remote`
**Dates:** `Dec 2025 – Present`

**Description** (те же правила формата — пустые строки и `▸`, без markdown):
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

**Skills (кнопка «Add skills» внутри записи):** `Go` · `Rust` · `Distributed Systems` · `Microservices` · `gRPC` · `PostgreSQL` · `Software Architecture` · `Platform Engineering`

---

## 6. Experience — блок 2: консалтинг

`Карандаш на записи Analyzit`

**Title:**
```
Data Architect & BigQuery Consultant
```

**Employment type:** `Part-time`
**Dates:** `Sep 2023 – Present`

**Description:**
```
A separate, part-time engagement alongside my main role — the data layer, where the money leaks.

▸ Cut a client's cloud bill by up to 10x by redesigning the BigQuery SQL and data layer: partitioning, clustering, materialised aggregates, and removing the full-scan queries that were quietly funding Google.

▸ Compressed client onboarding from 1–2 hours to 15 minutes by turning a manual launch checklist into an engineered workflow.

▸ Designing a SaaS backend that replaces Make/Zapier glue with explicit contracts, retries, idempotency and observability.

References available on request.

BigQuery · PostgreSQL · SQL · GCP
```

⚠️ **Обязательно проставить `Part-time`.** Без этого запись читается как второй фултайм параллельно текущему — это первое, за что цепляется рекрутер.

---

## 7. Experience — блок 3: Lenvendo

`Карандаш на записи Lenvendo`

**Title:**
```
Senior Backend Engineer / Team Lead
```

**Dates:** `Nov 2021 – Aug 2023`

**Description:**
```
Modular ecommerce engine, later spun out as a SaaS.

▸ Designed the modular core — clean Symfony layering, domain-driven module boundaries, async over Kafka and RabbitMQ — so a new client vertical is a module rather than a fork.

▸ Led a backend team of up to 6: code review, hiring filter, mentorship. Several juniors graduated into solid mids.

▸ Worked the product side directly with PM and client — roadmap, demos, specs and scope negotiation, including the unglamorous half: refusing features that would have made the engine unmaintainable.

PHP/Symfony · PostgreSQL · Redis · RabbitMQ · Kafka · Kubernetes
```

---

## 8. Experience — блок 4: Seowork ⚠️ главная правка

`Карандаш на записи SEOWORK.official`

Сейчас там: **CTO, Aug 2018 – Aug 2021**. Даты верные, но текст говорит «after eight years» и спорит с ними, а со-основательство не названо. Исправить:

**Title:**
```
Co-founder & CTO
```

**Dates:** `Aug 2018` – `Aug 2021`

**Description:**
```
Technical co-founder of the spin-out that turned the search analytics platform into a standalone SaaS, alongside the business founder, and CTO through to a successful exit in 2021 — eight years on the same product, from the first line of collection code in 2013 (Webit, then 404 Group) to the exit.

▸ Wrote ~70% of the backend personally — PHP first, then Go on the hot paths as volume outgrew the original design.

▸ Scaled query collection 40x, from 30,000 to 1,300,000+ per day per search engine. Google, Yandex and others each ran at that volume; aggregate collection was several times higher. No big-bang rewrite — the data layer evolved release by release while the product stayed up.

▸ Built the pipeline that consumed all of it: ingestion, deduplication, normalisation, classification, scoring, materialised aggregates, retention.

▸ Won and kept enterprise clients including Ozon and M.Video, whose SEO teams made daily calls on our data — which set the reliability bar for everything else.

▸ Grew the team from 1 to 10 (6-7 backend, 2-3 frontend, 1 QA), owning hiring, one-to-ones, architecture review and the on-call rotation.

▸ Owned the product, not just the stack — pricing, roadmap and release strategy with the CEO.

PHP · Go · MySQL/PostgreSQL · Redis · RabbitMQ
```

---

## 9. Experience — блок 5: NetByNet (добавить)

`Experience → «+» → Add position`

Сейчас этого места в LinkedIn нет вовсе — а это восемь лет и начало карьеры.

**Title:**
```
Developer, Corporate Reporting & Internal Systems
```
**Company:** `NetByNet`
**Dates:** `2005` – `Apr 2013`

**Description:**
```
Eight years at a national ISP, from the phone to the codebase — call-centre operator, field service, customer-facing and internal technical support, then development.

As a developer I built the corporate reporting systems the company's business analysts ran on: IFRS and RAS financial reporting, KPI tooling, and custom call-centre software on Asterisk.

Where I learned that the database is the soul of the product, and that most operational pain is a bad query wearing a costume.
```

**Почему коротко.** Это 2005–2013 — глубина деталей уже никого не интересует. Ценность блока в трёх вещах: восемь лет непрерывного стажа, рост от телефона до разработчика (читается как характер), и корпоративная отчётность IFRS/RAS, которой пользовались бизнес-аналитики — то есть аналитика и данные с самого начала карьеры. Больше писать не надо.

---

## 10. Experience — блок 404 Group: вернуть с правильными датами

`Experience → + → Add position`

**Решение изменено: запись возвращается, но с датами `Jul 2015 – Jul 2018`.** Внахлёст она висела из-за неверного периода, а не потому, что лишняя: без неё в профиле дыра `Apr 2013 → Aug 2018`. Готовый текст блока — `cv/09-опыт-2013-2018-и-netbynet.md`.

---

## 11. Featured ⚠️ сюда идут статьи

`Featured → «+» → Add a link`

Добавить **три** элемента, именно в этом порядке:

**1. Серия статей** — самый сильный элемент профиля после экзита.
- **Link:** ссылка на профиль dev.to (или на серию «Breaking the Monolith»)
- **Title:** `Breaking the Monolith — a 16-part engineering series`
- **Description:** `Splitting a live PHP monolith into Go microservices, written from inside the process: cutover without a flag day, identity ownership, sagas, gateways, Snowflake IDs, platform runtime.`

**2. Платформенная архитектура**
- **Link:** `https://github.com/brilliant-almazov/brilliant-almazov`
- **Title:** `Platform architecture — full technical breakdown`
- **Description:** `Distributed system map, platform library design, migration strategy, quality standards. The systems, in detail.`

**3. Open source**
- **Link:** `https://github.com/brilliant-almazov/metrics-bridge-rs`
- **Title:** `metrics-bridge-rs — Rust Prometheus exporter`
- **Description:** `Sub-millisecond responses against 50–200 ms through PHP. 12,500+ RPS with caching, verified across Redis, Dragonfly, Valkey and KeyDB.`

---

## 12. Статьи — отдельно про то, зачем это в профиле

Шестнадцать опубликованных частей серии — это не хобби, это **самый недооценённый актив профиля**.

Что видит читатель, которому ты в такой профиль попал:

- **Инженерный менеджер** — что ты умеешь формулировать решение, а не только его принимать. Человека, который написал «Flipping the Master Live», не надо спрашивать, понимает ли он риски cutover'а: он их разобрал письменно на публику.
- **Рекрутер** — сигнал seniority, который не подделывается. Резюме пишут все; шестнадцать технических статей — нет.
- **Команда, куда ты идёшь** — готовый ответ на «а как он объясняет сложное». Это ровно та компетенция, которую ждут от tech lead и architect, и её обычно проверяют на интервью вслепую.

Отдельно про Израиль: местный рынок маленький и очень networked, публичный технический след здесь работает сильнее, чем в большом рынке. Тебя находят по статье, а не по отклику.

**Дополнительно (не в профиль, а в привычку):** каждую новую опубликованную часть постить отдельным постом в LinkedIn — 3–4 абзаца по существу плюс ссылка на dev.to. Это единственный способ, которым профиль работает сам, пока ты занят кодом.

Темы опубликованных частей, если понадобится составлять список:
`a 200 OK that saved nothing` · `parallel-run consistency` · `identity ownership` · `stateless Go cascade` · `zero-downtime cutover` · `inter-service communication` · `saga / distributed transactions` · `Snowflake: why int8` · `Snowflake ID boundaries` · `public and internal gateways` · `Postgres enums / pgenum` · `services must be copy-paste` · `platform owns the runtime` · `auditing your own runtime` · `one generic core, not many copies` · `code moves both ways`

---

## 13. Skills — порядок важен

`Skills → «+» → добавить, затем Reorder`

**Top 3 (закрепить именно эти, они показываются в превью):**
```
Distributed Systems
Software Architecture
Go (Programming Language)
```

**Дальше в этом порядке:**
```
Platform Engineering
Microservices
PostgreSQL
gRPC
Rust (Programming Language)
Event-Driven Architecture
Message Queues (RabbitMQ, NATS, Kafka)
BigQuery
Data Pipelines
Scalability
System Design
Technical Writing
PHP
Symfony
Redis
Docker
Kubernetes
Google Cloud Platform (GCP)
CI/CD
Observability (Prometheus, Grafana)
Technical Leadership
Mentoring
```

Сейчас в топе стоят `Rust`, `Go`, `Distributed Systems`. Меняем на `Distributed Systems` + `Software Architecture` первыми — это роль, в которую идёшь, а не язык, на котором пишешь. `Technical Writing` добавлен под серию статей.

---

## 14. Languages

`Languages → карандаш`

- `Russian` → **Native or bilingual**
- `English` → **Professional working** ← поменять с `Limited working`
- `Hebrew` → **Elementary**

`Limited working` в глазах рекрутера — стоп-сигнал до разговора. `Professional working` соответствует реальности: читаешь, пишешь, ревьюишь и работаешь асинхронно на английском ежедневно, и публикуешь технические статьи на английском. Разговорную беглость дорабатываешь — это нормально обсудить голосом, а не отсекать себя строкой в профиле.

---

## 15. Что убрать из профиля

- `3.4M LOC` и `6,300 commits` из headline и summary. Метрика не врёт, но у неё свой читатель: в GitHub-профиле она стоит рядом с coverage floor, hooks и real-infra тестами — там видно, что объём не стал долгом. В LinkedIn этого контекста нет, и она читается как «AI навалил кода». Место ей — в `docs/ai-engineering.md`, куда придут за подробностями.
- Ссылку на LinkedIn Натана Крейдермана из описания Analyzit. Рекрутеру неважно, *с кем*; важно, *что получилось*. Партнёрство упоминается через `References available on request`.
- Шесть из семи ссылок на GitHub в контактах — оставить профиль и главный репозиторий, остальное живёт в Featured.
- `Gaming Vertical` из названия текущего места. Компанию не палим, индустрию достаточно назвать в описании, а именно эта вертикаль у части работодателей вызывает лишний вопрос.

---

## 16. Порядок действий

1. Headline + Location + Open to work — 5 минут, даёт больше всего.
2. Seowork: даты и title (блок 8) — самая крупная потеря веса в текущем профиле.
3. Featured: серия статей первым элементом (блок 11).
4. Удалить 404group, добавить NetByNet.
5. Analyzit → `Part-time`.
6. About.
7. Skills — порядок.
8. Language: English → Professional working.

Первые пять пунктов — примерно двадцать пять минут, и профиль перестаёт противоречить резюме.
