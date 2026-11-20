<a href="https://brilliant-almazov.com/en/"><img src="docs/images/site/hero-planet.webp" alt="Monolith City: settlements, roads of letters and the portal under a starry sky" width="100%"></a>

# Anton Brilliantov

### 🌐 [brilliant-almazov.com](https://brilliant-almazov.com/en/)

**Distributed Systems Architect · Engineering Leader · Ex-CTO & Co-founder (SaaS)**
I design distributed systems and build the teams that run them.

📍 Ramat Gan, Israel · Open to architecture, platform, data-platform and engineering leadership roles
🌐 [Site](https://brilliant-almazov.com/en/) · ✉️ brilliantov.anton@gmail.com · 💼 [LinkedIn](https://www.linkedin.com/in/anton-brilliantov) · ✍️ [dev.to](https://dev.to/anton_brilliantov) · 🐙 [GitHub](https://github.com/brilliant-almazov)

<p>
<a href="https://brilliant-almazov.com/en/"><img src="https://img.shields.io/badge/site-brilliant--almazov.com-2f6f8f?style=flat-square" alt="Site"></a>
<a href="#writing"><img src="https://img.shields.io/badge/writing-dev.to-3b4a5a?style=flat-square" alt="Writing"></a>
<a href="#monolith-city"><img src="https://img.shields.io/badge/world-Monolith%20City-6b7f3a?style=flat-square" alt="Monolith City"></a>
<a href="#the-keepers-family"><img src="https://img.shields.io/badge/cast-the%20Keeper's%20family-8a6a3a?style=flat-square" alt="The Keeper's family"></a>
</p>

---

## In short

- **Built SEOWORK from the first line of code to my exit in 2021** as technical co-founder and CTO: collection scaled 40x to 1.3M+ queries/day per search engine, engineering grew from 1 to 10, enterprise clients included Ozon and M.Video. The platform still runs today.
- **Now:** founding engineer and platform architect of an early-stage startup in stealth. ~20 Go services and 100+ production components in under a year, with two engineers.
- **Data is the thread:** from board-level reporting, to high-volume collection pipelines, to a BigQuery redesign that cut a client's bill by up to 10x.

---

## What I'm building now

An early-stage startup in stealth. A well-structured Symfony monolith is being replaced service by service, for resource efficiency and independent scaling.

- **Go platform library** every service imports: lifecycle, gRPC/HTTP/Postgres/NATS/RabbitMQ/Redis, transactional outbox, Snowflake IDs, observability, testcontainers harness. New service to production in a day.
- **~20 microservices in production** across 35+ repositories, each shipping as gRPC server, worker, outbox and scheduler binaries. I design, build, deploy and operate them.
- **Analytical data layer**: ingestion and transformation pipelines from crawled and third-party sources.
- **Control plane**: service registry with mutual Ed25519 auth; admin with RBAC and audit trail.
- **Contracts as artefacts**: shared Protocol Buffers repo generating Go and PHP stubs.
- **Delivery**: CI/CD across 35+ repositories, 90% coverage gates, integration tests on real infrastructure, image-size budgets on every PR.

| Measured | Before | After |
|---|---|---|
| Memory per worker | ~150 MB (Symfony) | ~20 MB (Go), ~7x |
| Container image | 100+ MB | 20–30 MB, 5–10x |
| Metrics scrape | 50–200 ms | sub-millisecond |
| New service to prod | ~1 week | 1 day |

### Deep dives

| Document | What it covers |
|---|---|
| [architecture.md](docs/architecture.md) | System map, layers, outbox → NATS |
| [platform.md](docs/platform.md) | Go library, registry, service template |
| [migration.md](docs/migration.md) | PHP → Go: reasoning, method, measured savings |
| [admin-operations.md](docs/admin-operations.md) | Control plane: RBAC, audit, operations workflows |
| [ai-engineering.md](docs/ai-engineering.md) | How a two-person team ships safely with AI agents |
| [quality-standards.md](docs/quality-standards.md) | The enforced rule-book |

---

## Career

**Founding Engineer & Platform Architect** · Stealth Startup · Remote · Dec 2025 – present
Architecture, platform, delivery and technical roadmap.

**Data Architect & BigQuery Consultant** · Analyzit · Sep 2023 – Dec 2025
Up to 10x lower BigQuery bill; client onboarding from 1–2 hours to 15 minutes; designed and built the Data-Masters dashboard suite from scratch.

**Senior Backend Engineer / Team Lead** · Lenvendo · Nov 2021 – Aug 2023
Modular e-commerce core over Kafka and RabbitMQ; led a team of up to 6.

**SEOWORK — one company, three stages, eight years** · 2013 – 2021
- **Co-founder & CTO** · 2018 – 2021 · standalone company, organic growth · exited 2021
- **Head of Development** · 2015 – 2018 · inside 404 Group, venture-backed
- **Backend Developer** · 2013 – 2015 · in-house platform at the Webit agency; clients were billed on its data

Grew engineering 1 → 10. Scaled collection 40x without a big-bang rewrite; terabytes of data in MySQL, sharded by logical tables. Built the full pipeline: ingestion, deduplication, normalisation, classification, scoring, aggregates, retention. European Search Awards finalist 2021. Owned pricing and roadmap with the CEO.

**Support → Network Engineer → Developer** · NETBYNET · 2005 – 2013
Eight years, six roles, ending in the corporate reporting the board relied on.

---

## Open source

- [**metrics-bridge-rs**](https://github.com/brilliant-almazov/metrics-bridge-rs) · Prometheus exporter for PHP metrics in Redis. Sub-millisecond vs 50–200 ms through PHP, 12,500+ RPS.
- [**pgenum**](https://github.com/brilliant-almazov/pgenum) · Go · Runtime management of PostgreSQL ENUM types, zero dependencies.
- [**railway-exporter-rs**](https://github.com/brilliant-almazov/railway-exporter-rs) · Prometheus exporter for Railway.app billing.

---

## Writing

Articles by a software engineer, about one idea at a time: real decisions, told through a small cast of characters. Read them on [dev.to](https://dev.to/anton_brilliantov); the world, the map and the cast live on [brilliant-almazov.com](https://brilliant-almazov.com/en/).

### Live now

**Breaking the Monolith** · how a walled city is taken apart district by district without stopping it.

<a href="https://dev.to/anton_brilliantov/breaking-the-monolith-part-1-a-200-ok-that-saved-nothing-16ef"><img src="docs/images/writing/monolith-topology.webp" alt="Two engines, one database: the monolith and the new service during the cutover" width="100%"></a>

| Part | Article |
|---|---|
| 1 | [A 200 OK that saved nothing](https://dev.to/anton_brilliantov/breaking-the-monolith-part-1-a-200-ok-that-saved-nothing-16ef) |
| 1.5 | [Two rule engines, one truth](https://dev.to/anton_brilliantov/breaking-the-monolith-part-15-two-rule-engines-one-truth-4mhb) |
| 2 | [Who owns a hash function](https://dev.to/anton_brilliantov/breaking-the-monolith-part-2-who-owns-a-hash-function-4h3f) |
| 3 | [The cascade that timed out](https://dev.to/anton_brilliantov/breaking-the-monolith-part-3-the-cascade-that-timed-out-43pa) |
| 4 | [Flipping the master live](https://dev.to/anton_brilliantov/breaking-the-monolith-part-4-flipping-the-master-live-2kn9) |
| 6 | [Most "we need a saga" is really "we need idempotency"](https://dev.to/anton_brilliantov/breaking-the-monolith-part-6-most-we-need-a-saga-is-really-we-need-idempotency-2894) |

**Snowflake IDs** · [Part 1: Why int8 + Snowflake, and never UUID](https://dev.to/anton_brilliantov/snowflake-ids-part-1-why-int8-snowflake-and-never-uuid-1nb8)

<a href="https://dev.to/anton_brilliantov/snowflake-ids-part-1-why-int8-snowflake-and-never-uuid-1nb8"><img src="docs/images/writing/snowflake-bits.webp" alt="Bits of a Snowflake ID" width="70%"></a>

### Series written

Eleven series, each a short run of conceptual articles. New parts appear on [dev.to](https://dev.to/anton_brilliantov) and on [the site](https://brilliant-almazov.com/en/).

| | Series | | Series |
|---|---|---|---|
| 🧱 | Breaking the Monolith | ❄️ | Snowflake IDs |
| 🏭 | Platform and generation | 🤝 | Working with agents |
| 🧰 | Operations out of the box | 🧬 | Generics in Go |
| 📜 | From requirement to contract | 🔗 | Services and commitments |
| 🗝️ | Access, tracing, rollout | 🕳️ | Why there is no result |
| 🧪 | Testing production with an executor | | |

### Covers from the shelf

<table>
<tr>
<td width="50%"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/covers/token-at-the-edge.webp" alt="Access, tracing, rollout: the token stops at the edge" width="100%"></a></td>
<td width="50%"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/covers/contract-is-a-proto-file.webp" alt="From requirement to contract: the contract is a .proto file" width="100%"></a></td>
</tr>
<tr>
<td width="50%"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/covers/ownership-is-a-field.webp" alt="Services and commitments: ownership is a field, not an agreement" width="100%"></a></td>
<td width="50%"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/covers/accountability-stays-human.webp" alt="From requirement to contract: accountability stays human" width="100%"></a></td>
</tr>
<tr>
<td colspan="2"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/covers/planet-on-a-laptop.webp" alt="A planet on a laptop: continents, providers, datacenters and zones declared once" width="100%"></a></td>
</tr>
</table>

### In motion

Every article explains its idea with a small moving picture.

<table>
<tr>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/motion/quorum.gif" alt="Lose one zone, keep the majority" width="100%"></a><br><sub>Lose one zone, keep the majority</sub></td>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/motion/link-cut.gif" alt="Healing a site keeps the link cut" width="100%"></a><br><sub>Healing a site keeps the link cut</sub></td>
</tr>
<tr>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/motion/span-zone.gif" alt="Each span carries its zone" width="100%"></a><br><sub>Each span carries its zone</sub></td>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/motion/three-builds.gif" alt="What we own fell; the network never moved" width="100%"></a><br><sub>What we own fell; the network never moved</sub></td>
</tr>
<tr>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/motion/push-to-plan.gif" alt="A push, the stand, a row, the plan" width="100%"></a><br><sub>A push, the stand, a row, the plan</sub></td>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/motion/parcel-walk.gif" alt="The parcel walks the chain and back" width="100%"></a><br><sub>The parcel walks the chain and back</sub></td>
</tr>
</table>

<p>
<a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/venom-fork.webp" alt="We forked the test runner" width="49%"></a>
<a href="https://brilliant-almazov.com/en/"><img src="docs/images/writing/pr-body.webp" alt="One story, many readers" width="49%"></a>
</p>

---

## Monolith City

<a href="https://brilliant-almazov.com/en/game/"><img src="docs/images/writing/zoo-planet.webp" alt="The planet of settlements seen from above" width="100%"></a>

The world of the series. A planet of settlements: in the middle stands a monolith city, broken into districts, and every district is a microservice that keepers look after. Roads carry letters between them; the stars overhead are other people's systems.

- 🗺️ **[Game story](https://brilliant-almazov.com/en/game/)**: the interactive map of the planet.
- 📅 **[Seasons S1–S6](https://brilliant-almazov.com/en/game/seasons/)**: the story season by season, one arc per resident.
- 🏙️ **[Monolith City](https://brilliant-almazov.com/en/monolith/)**: the city itself, district by district.

<a href="https://brilliant-almazov.com/en/game/seasons/"><img src="docs/images/writing/story-map.webp" alt="The story so far: six seasons on one road" width="100%"></a>

<a href="https://brilliant-almazov.com/en/game/seasons/"><img src="docs/images/writing/arcs.webp" alt="How the characters grow" width="100%"></a>

### Life in the city

The residents explain the hard parts their own way: a queue is a line at the bakery, a shared database is a dragon everybody still borrows from, and one grumpy service makes the whole chain grumpy.

<a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/zoo.webp" alt="The residents of the city at the enclosure" width="100%"></a>

<table>
<tr>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/bakery-queue.gif" alt="A queue is a line at the bakery" width="100%"></a><br><sub>A queue is a line at the bakery</sub></td>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/spike.gif" alt="A spike, as Pickle sees it" width="100%"></a><br><sub>A spike, as Pickle sees it</sub></td>
</tr>
<tr>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/borrow-from-the-dragon.webp" alt="Everybody still borrows from the dragon" width="100%"></a><br><sub>Everybody still borrows from the dragon</sub></td>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/one-job-two-owners.webp" alt="One job, two owners" width="100%"></a><br><sub>One job, two owners</sub></td>
</tr>
<tr>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/grumpy-chain.webp" alt="One grumpy service, a grumpy chain" width="100%"></a><br><sub>One grumpy service, a grumpy chain</sub></td>
<td width="50%" align="center"><a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/courier-comic.webp" alt="The courier sniffs every lamppost" width="100%"></a><br><sub>The courier sniffs every lamppost</sub></td>
</tr>
</table>

<a href="https://brilliant-almazov.com/en/game/heroes/"><img src="docs/images/world/race.webp" alt="The hare and the tortoise race to the flag" width="100%"></a>

---

## The Keeper's family

<a href="https://brilliant-almazov.com/en/game/family/"><img src="docs/images/family/portrait.webp" alt="The Keeper's family at the portal, with the animals of the city" width="100%"></a>

The recurring cast of the articles. They meet the animals of the city at the portal and show up whenever a story needs a human view. All drawings are from [the site](https://brilliant-almazov.com/en/game/family/).

**The Keeper** · the author: long grey hair in a thick braid, round tortoiseshell glasses, a salt-and-pepper beard.

<table>
<tr>
<td align="center" width="20%"><a href="https://brilliant-almazov.com/en/game/family/"><img src="docs/images/family/sveta.webp" alt="Sveta" width="100%"></a><br><b>Sveta</b><br>the Keeper's wife</td>
<td align="center" width="20%"><a href="https://brilliant-almazov.com/en/game/family/"><img src="docs/images/family/lev.webp" alt="Lev" width="100%"></a><br><b>Lev</b><br>the Keeper's son</td>
<td align="center" width="20%"><a href="https://brilliant-almazov.com/en/game/family/"><img src="docs/images/family/nova.webp" alt="Nova" width="100%"></a><br><b>Nova</b><br>the Keeper's daughter</td>
<td align="center" width="20%"><a href="https://brilliant-almazov.com/en/game/family/"><img src="docs/images/family/misha.webp" alt="Grandpa Misha" width="100%"></a><br><b>Grandpa Misha</b><br>big grey walrus moustache</td>
<td align="center" width="20%"><a href="https://brilliant-almazov.com/en/game/family/"><img src="docs/images/family/lyolya.webp" alt="Lyolya" width="100%"></a><br><b>Lyolya</b><br>a fluffy tuxedo cat</td>
</tr>
</table>

---

## Engineering principles

- One way to do everything, enforced by the platform library.
- 90% coverage floor in CI; floors only go up.
- Integration tests on real Postgres, NATS and RabbitMQ. Never mocks for infrastructure.
- Schema-first contracts: shared protos, forward-only migrations.
- Zero defaults in shared libraries: a missing config fails at start, not in production.
- AI executes; architecture decisions stay human.
- No standing production access for agents: granted deliberately, per task, only when needed. Critical operations stay hands-on.

---

**Languages:** English (professional), Russian (native), Hebrew (learning).
