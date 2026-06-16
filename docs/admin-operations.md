# Admin & operational control plane

> **Why this exists:** in a serious production environment, **engineers do not have direct database access**, **do not SSH to containers** and **do not run ad-hoc SQL in prod**. They need a tool. The admin panel *is* that tool — the only sanctioned way to inspect, modify and operate the platform without writing a one-off script or pinging an on-call engineer.

This is not "an admin CRUD". It's a **platform-wide operational control plane** with access control, audit, safety rails and structured workflows.

---

## What it solves

| Pain | How admin solves it |
|---|---|
| "I need to look at table X" | Browse it through the admin DB inspector — read-only, no `psql` needed, no risk. |
| "I need to update a row" | Edit it through the admin form, with validation, confirmation, and a permanent audit-log record of who, what, when, why. |
| "I deleted the wrong row" | Soft-delete is the default. The row is hidden, not gone. One click to restore. Hard delete exists but requires explicit confirmation and is irreversible. |
| "I need to run a migration / archive / smart copy" | Operations tab — pre-defined, audited, parameterised. No bash. |
| "I need to see why the system is in this state" | Audit log with field-level diffs and clickable reference resolution (FK IDs are shown as the referenced object). |
| "I need to add a colour to a status badge" | Dictionary editor + enum styles — change UI semantics through admin, no code change. |
| "I don't trust giving access to junior engineers" | RBAC. The same panel, with permissions scoped per role. |

---

## What it actually does

### 1. Database inspector across every service DB

- Reads PostgreSQL metadata across every service database (config DB and read-only data sources).
- Auto-discovers tables, columns, FKs, enums, indexes from `information_schema`.
- YAML table configs (`config/tables/`) layer on top: which columns to show, which to make editable, references, enums, filters, column groups.
- Filters and sort live in the URL — every query is a shareable link.

### 2. Audit log — the platform's memory

Every write through admin is recorded. **Field-level diffs**, **reference resolution**, **author tracking**, **action semantics**.

- Action semantics:
  - `insert` — creation of an entity.
  - `update` — change of fields. Diff stores **only changed fields**.
  - `delete` — soft delete (`is_active = false`). Row stays in the database.
  - `remove` — hard delete. Row is gone forever.
- Reference resolver. When a row has a `dictionary_entry_id: 129`, the audit record also carries the resolved object: `dictionary_entry: { code: "black", label: "Black", ... }`. So a year later, when the row IDs have been re-mapped or archived, the audit record is still readable.
- DiffView (UI). JSON with colour-coded fields:
  - Changed primitive: red (Was) / green (Now).
  - Reference object: orange background.
  - Unchanged fields: grey (context).
  - Insert: only Now (green). Delete / Remove: only Was (red).

### 3. RBAC + auth (Zitadel)

- Authentication via Zitadel. SSO with the company IdP.
- Role-based access control on the admin BFF side. Read-only roles for analysts, write for operators, destructive (hard delete, migrations) for senior engineers only.
- Session-bound. CORS, SSE fan-in, rate limit and telemetry all live in the gateway in front of the BFF — see [refactoring plans](./refactoring-plans.md) for how this is split out.

### 4. Operations: real workflows, not ad-hoc scripts

The "Operations" area exposes pre-defined, parameterised, audited jobs. No one is running `pg_dump` from a laptop.

- **Smart copy** — copy a table (or a subset) between data sources with mapping and filtering.
- **Archive** — move old rows out of the hot table into the archive schema. Triggered manually or scheduled.
- **Migrator** — run platform-level migrations. Currently a standalone binary, being merged into ops-svc — see [refactoring plans](./refactoring-plans.md).
- **Scheduled jobs** — UI to inspect, pause, replay and reschedule.
- **Job history** — every run has its parameters, duration, outcome and operator stored.

### 5. Configuration as data

- **Dictionaries.** Free-form key/value sets used as enum sources across the platform (statuses, categories, brands, regions). Editable through admin with `display_type` per entry: `color_badge`, `icon`, `default`.
- **Enum styles.** Global per-PG-enum colour mapping (Mantine palette: gray, red, pink, grape, violet, indigo, blue, cyan, teal, green, lime, yellow, orange, dark). Change once, applied everywhere the enum appears in any admin table.
- **Preferences.** Per-user UI state — column visibility, default filters, saved views — stored server-side, synced across devices.
- **Releases / changelog.** `docs/releases.json` is admin-served, with bilingual (en + ru) entries per release, scoped by `api` / `ui` / `both`.

### 6. Two-database isolation

- **Config DB** — admin's own PostgreSQL. Stores table configs, enum styles, preferences, audit log, RBAC data.
- **Data sources** — **read-only** PostgreSQL connections to every service's DB. Admin reads through them; it never writes there directly. Writes happen via the service's gRPC API or via the operations workflows.

This split is a hard safety rail: even if the admin code has a bug, it cannot corrupt service data — the connection is read-only at the role level.

### 7. Observability of the platform itself

- Reads the **control-plane registry** to show live state of every service replica: status (`healthy / unhealthy / dead`), uptime, last heartbeat, address.
- Proxies sidecar commands through the registry: start / stop / restart / scale a process, view live logs (SSE).
- Grafana dashboard links per service, per replica.
- Cross-service search by request ID (via trace context).

---

## Why this is a platform feature, not an app feature

Every service in the system **leans on the admin** for:

- **Operability without engineers.** PMs, support, ops can do their job. Engineers do not get paged for "please update row X".
- **A single audit trail.** All "who changed what" lives in one place, regardless of which service owns the data.
- **Safety.** Soft vs hard delete, confirmation dialogs, RBAC, read-only connections to service DBs — it's structurally hard to do damage.
- **Configurability.** Adding a new dictionary, tweaking enum colours, changing column visibility — none of it requires a deploy.

This is why **the admin is treated as part of the platform**, not as a per-service ornament. Its refactoring plan (gateway + 5 backend services + microfrontends) is in [`docs/refactoring-plans.md`](./refactoring-plans.md).

---

## Stack

- **Backend:** Go (Chi router, pgx), gRPC clients to every service, Postgres for the config DB, Redis cache (warmed on startup, invalidated on write).
- **Frontend:** React 18 + Vite + TypeScript + Mantine v7 + Refine.dev + React Query. No global state library — server state belongs to React Query, URL state belongs to the URL.
- **Auth:** Zitadel (SSO).
- **Observability:** every admin write produces an audit row + a Prometheus counter.
- **Deploy:** Nginx serves the SPA, reverse-proxies `/api/*` to the Go BFF. Two images, ~23 MB API + ~47 MB UI, ~70 MB total.
