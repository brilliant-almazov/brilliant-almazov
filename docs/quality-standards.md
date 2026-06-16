# Hard quality standards

> Codified in per-repo `CLAUDE.md` files and enforced by `PreToolUse` / `PostToolUse` hooks. AI cannot drift; humans cannot forget.

These are not guidelines. They are the rules every commit obeys, in every repository, on this platform.

---

## Universal (every repository)

| Rule | Why |
|---|---|
| **Branch naming:** `<type>/<ticket-id>-<short-desc>` (`feat`, `fix`, `hotfix`, `refactor`). No username prefixes. | Predictable filtering, scriptable CI, no "whose branch was that?". |
| **Commit type whitelist:** `feat`, `fix`, `hotfix`, `refactor`, `test`, `docs`, `style`, `perf`, `ci`. `chore:` is **forbidden**, globally. | "Chore" means "I didn't think about what kind of change this is". Every change has a real type. |
| **PR title format:** `<type>(<scope>): <description> (<TICKET-ID>)` — ticket ID in the title, in parentheses, always. | Trivial to cross-reference Linear from a PR list. |
| **No AI attribution** in commits, PRs, code or comments. No `Co-Authored-By: Claude`, no "Generated with Claude Code". | The engineer owns the change. Period. |
| **Linear assignee + estimate + status discipline.** Every task gets an estimate; assignee is moved to "me" on first action; status follows the work (`In Progress` → `Review` → `Done` / `Blocked`); budget reported on close. | Visibility for the team without manual standup overhead. |
| **`master`/`main` is protected.** No direct push, no skipped hooks, no force-push to shared branches. PRs only, and only the human merges. | Auditability. No "I'll just hotfix master real quick". |
| **No secrets in commits.** `.env`, credentials, tokens never land in git. Hooks block them. | Self-explanatory. |

---

## Go

### Architecture

- **OOP, interface-driven.** Even a single implementation gets an interface. No procedural / functional package layout in shared code.
- **Dependencies through interfaces, never concrete types.** No `switch` on concrete type in shared code — use polymorphism.
- **No `helpers.go` / `utils.go` / `funcs.go`.** Any operation is a method on a struct. If the struct is "artificial", the design is wrong — find the real abstraction.
- **Transactions are struct fields, not function arguments.** `func Do(ctx, tx pgx.Tx, ...)` is **forbidden**. The right shape: a struct whose executor (pool or tx) is a field; `WithTx(tx) *Type` returns a scoped instance for a transaction; transaction-management lives inside a method (`Store.RunInit(ctx, fn)` opens / commits / rolls back). Outside, no one sees a `pgx.Tx`.
- **`errors.Is` / `errors.As` only.** Never direct comparison (`err == X`) or type switch on errors. Even after `errors.As(err, &errno)`, comparisons stay tagless: `switch { case errors.Is(errno, syscall.ECONNRESET): ... }`. **Global** rule across all Go projects.
- **No hardcode in shared libraries.** Exchange names, queue names, bus names, FQCN, format strings, timeouts — every value comes from `Config` or an `Option`, with **no defaults**. The caller must pass it. Forgetting fails the boot, not production three weeks later.

### Layout

- **One struct per file**, file named after the struct. Helpers belong in their own file too. Methods of one entity spread across `<entity>_run.go`, `<entity>_dispatch.go`, etc.
- **Max 100 lines per file** for new Go code. Existing larger files get refactored gradually. If you need to scroll, the file is too big.
- **One Config per service.** `internal/config/config.go` with nested slices. No per-package `Settings` / `Config` structs.
- **No local "compat" interfaces.** `httpHandlerCompat`, `moduleCompat`, mirrors of platform types — forbidden. Import the platform contract directly: `var _ platform.X = (*T)(nil)`.

### Testing

- **`testcontainers-go` for infra-touching tests.** Real Postgres, real NATS, real RabbitMQ — never mocks.
- **One container per test run.** Not per test. Not per package. One `Run()` boots a Postgres / NATS / RabbitMQ once; all packages share it via env vars. External bootstrap script with `trap EXIT` teardown.
- **Isolation between tests at the data layer.** Per-test schema / namespace / database name. Pristine setup; `DROP` on cleanup.
- **`-p 1` for NATS JetStream** (no overlapping subjects across parallel test packages).
- **Explicit `t.Cleanup` for every JetStream stream / queue created.** No leaks.
- **No `time.Sleep` for readiness.** Use `WaitingFor` / log-wait / health-check polling.

### Errors & control flow

- **`errors.Is` / `errors.As` everywhere** (already listed above — it's that important).
- **Wrap with `%w`** when adding context to an error.
- **`samber/oops` / `samber/mo`** acceptable where they pull weight; no procedural drift.

---

## Frontend (Go BFF + React)

### File layout & imports

- **`@-aliases` only:** `@components/`, `@hooks/`, `@pages/`, `@providers/`, `@routes/`. Never `../`.
- **Max 100 lines per component file** (imports included). Decompose into atoms / molecules — no monoliths.
- **Three layers minimum** for non-trivial pages: (1) data hook, (2) page-controller hook composing data hooks + URL state, (3) dumb renderer. Pages must not call `useQuery` directly.

### Hooks

- **Explicit return types on hooks** that return objects. The interface lives in `@models/`, not in the hook file. No inferred anonymous-object types.
- **Smart / dumb split.** Render components are dumb: only `props → JSX`, zero hooks, zero logic. Data fetching and state live in separate hooks (`use*.ts`). Pages compose smart hooks + dumb renderers.

### Data & rendering

- **React Query only** for data fetching. **Never** raw `fetch()` in components.
- **Use the project's `api` client** (`@hooks/useApi` → `api.get/put/post/delete`) inside `queryFn` / `mutationFn`.
- **Filters and sort live in the URL.** Everything reproducible by sharing a link.
- **No `.map()` in JSX.** Use `<Each items=… render=… />`. Maps belong in hooks / transformers, not in render.
- **No ternaries / `&&` in JSX.** Use `<Show when=… fallback=… />`.
- **No duplicated utilities.** Before adding `formatBytes`, `formatUptime`, clipboard, etc., grep `ui/src` for an existing implementation.
- **Deletions always with confirmation.** Soft (hide) and hard (permanent) are visually and semantically different.
- **Mantine components only.** No custom CSS files unless absolutely required.

---

## Database & migrations

- **Snowflake `BIGINT` IDs everywhere.** Never `SERIAL`, never `BIGSERIAL`. The only exception is goose's own service table.
- **`TIMESTAMP(6) WITHOUT TIME ZONE`, UTC.** Always.
- **`created_by` NOT NULL, `updated_by` DEFAULT NULL, `created_at` NOT NULL DEFAULT NOW(), `updated_at` DEFAULT NULL.** Strict order, always at the end of the table.
- **Append-only audit tables:** `author` + `created_at`, no `created_by` / `updated_by`.
- **`COMMENT ON COLUMN` required for every column.** No exceptions.
- **`VARCHAR` not `TEXT`. `INET` for IPs. PostgreSQL native `ENUM` types** wherever possible. No string-coded enums.
- **Audit / log tables live in the `audit` schema.** Their enum types too.
- **One migration = one semantic action.** `CREATE TYPE` is one file; `CREATE TABLE` + indexes is another; `INSERT` seed is a third.
- **Forward-only migrations.** No `down`. Rollbacks are new forward migrations. `NEVER DROP COLUMN` in shared schemas — use `RENAME` + `ALTER TYPE`.
- **Indexes only with a known query pattern.** Never "by hunch". No query → no index. Hunch indexes are net negative.
- **Repeated strings (`key_path`, etc.) get a reference table** + `key_id BIGINT`. No magic strings in 50M rows.
- **`goose` (Pressly) + `embed.FS`** is the standard migration runner. After `Up()`, the `goose_db_version` table gets a `name` column derived from the filename — far easier to read than goose's default `tstamp`.

---

## SQL formatting (when reading / authoring it by hand)

All SQL is formatted in a strict "ladder" style:

- `SELECT`, `FROM`, `WHERE`, `GROUP BY`, `ORDER BY`, `HAVING`, `LIMIT` — each on its own line.
- Contents on the next line, indented +4.
- Each `SELECT` column on its own line.
- `INSERT … SELECT`: every selected value has a `-- target_column_name` trailing comment.
- Each CTE (`WITH … AS`) follows the same rules.
- Large-table joins: `ON` on the same line, `AND` aligned underneath.
- Window functions: `PARTITION BY` and `ORDER BY` inside `OVER()` go on their own lines.
- Join conditions: indexed columns first; non-indexed (e.g. `domain_id`) last.

These are not stylistic preferences — they're how the team reads SQL during code review without losing track of which `WHERE` belongs to which `SELECT`.

---

## Observability — non-negotiables

- **Every driver, pool, client publishes Prometheus counters and histograms per operation.** `received_total`, `acked_total`, `naked_total`, `published_total`, `handler_seconds_*`, etc. Nil-safe (no `nil` metric pointer panics). No "we'll add metrics later".
- **Structured logs (`zap`), JSON format, trace-context-aware.** Every log line carries the request / trace ID.
- **`/metrics`, `/healthz`, `/readyz`** on a separate system port. Always.

---

## Grafana dashboards

- **Colours: `palette-classic` only.** No custom colours, no per-series overrides.
- **`gradientMode: none`. `fillOpacity: 0`.** Clean lines, no fills.
- **Stat panels:** `mode: thresholds` (green / yellow / red).
- **Uptime format:** `dtdurations` (`1h 25m`, `5d 3h`, `1M 5d`) everywhere.

Before creating a new dashboard, copy the style from an existing one. First time right.

---

## Process discipline (Linear + GitHub)

- **Estimate every task.** No story is "no estimate". 1 pt ≈ 1h of Claude execution.
- **Status moves the moment the work moves.** PR open → `In Review`. PR merged → `Done`. Blocked → `Blocked`. No batching.
- **Budget tracking comment on every task** — time, tokens, money, ops, incidents, estimate vs actual.
- **Incident logging in-line:** Claude mistakes, scope changes, spec ambiguity, tech surprises, dependency blocks — each is its own structured comment in the moment, not post-hoc.
- **Atomic commits.** One semantic change per commit. Refactor + feature in the same commit is rejected at review.
- **No `Co-Authored-By: Claude`.** Already mentioned. Worth re-stating.

---

## What these rules buy

- **Code review is fast.** Most categories of mistake are blocked by hooks before they reach a reviewer.
- **Onboarding is fast.** A new agent (human or AI) reads `CLAUDE.md` and is productive in an hour.
- **Refactors are safe.** Migrations are forward-only and predictable; types and contracts are explicit.
- **Failure is observable.** Every operation produces a metric and a log line; there are no silent failures.
- **The codebase ages slowly.** No `chore` commits, no `utils.go` graveyards, no "we'll figure out a Type for it later" anonymous objects in React state.
