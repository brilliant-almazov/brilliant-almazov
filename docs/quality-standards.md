# Hard quality standards

> Codified in per-repository convention files and enforced by tooling hooks. Automation cannot
> drift; people cannot forget.

These are not guidelines. They are the rules every commit obeys, in every repository.

---

## Universal

| Rule | Why |
|---|---|
| **Branch naming:** `<type>/<ticket-id>-<short-description>` (`feat`, `fix`, `hotfix`, `refactor`). No username prefixes. | Predictable filtering and scriptable CI. |
| **Commit type whitelist:** `feat`, `fix`, `hotfix`, `refactor`, `test`, `docs`, `style`, `perf`, `ci`. `chore:` is forbidden. | "Chore" means the author did not decide what kind of change this is. |
| **PR title format:** `<type>(<scope>): <description>` with the issue reference. | Cross-referencing a PR list to the work it came from is trivial. |
| **No AI attribution** anywhere — commits, PRs, code, comments. | The engineer owns the change. |
| **`master` is protected:** no direct push, no force-push to shared branches, no skipped hooks. Pull requests only, merged by a human. | Auditability. |
| **No secrets in commits.** Credentials and environment files never land in git; hooks block them. | Self-explanatory. |

---

## Go

### Architecture

- **Interface-driven.** Even a single implementation gets an interface; dependencies are taken
  as interfaces, never as concrete types.
- **No `helpers.go` / `utils.go`.** An operation is a method on a type. If the type feels
  artificial, the abstraction has not been found yet.
- **Transactions are struct fields, not arguments.** `func Do(ctx, tx, …)` is forbidden: the
  executor is a field, a `WithTx` constructor returns a scoped instance, and transaction
  management lives inside a method. Callers never see a transaction handle.
- **`errors.Is` / `errors.As` only.** Never `err == X`, never a type switch on errors.
- **No hardcoded values in shared libraries.** Names, timeouts and formats come from config or
  options, with no defaults — a missing value fails the boot, not production.

### Layout

- **One type per file**, named after the type; methods of one entity split across suffixed
  files.
- **Small files.** New code stays under a hundred lines per file; scrolling means the file is
  doing too much.
- **One config per service**, not a settings struct per package.
- **No local compatibility shims** that mirror platform types — import the contract.

### Testing

- **Everything is tested:** handlers, consumers, repositories, workers, mappers.
- **A coverage floor per package, enforced in CI.** Below the floor the pipeline is red and the
  PR is blocked. Floors ratchet up, never down; lowering one requires a written reason.
- **Real infrastructure in integration tests** through testcontainers: real database, real
  broker. Never mocks for infrastructure.
- **One container set per test run**, with per-test schema or namespace isolation and explicit
  cleanup of everything created.
- **No sleeps for readiness** — wait on health, logs or conditions.
- **Integration tests for anything crossing a boundary;** unit tests for pure functions.
- **Table-driven by default**, especially for converters, validators and state machines.
- **No flaky-test culture.** A flaky test is a broken test: quarantine for 48 hours, then fixed
  or deleted.

### Errors and control flow

- **Wrap with `%w`** when adding context; sentinel errors are compared, not parsed.
- **Errors carry a class**, so a caller decides by class rather than by message text.
- **Context first** in every signature that can block, and cancellation is honoured.

---

## Data

- **Forward-only migrations**, immutable once merged.
- **Every column documented** in the migration that creates it.
- **Sortable 64-bit IDs** instead of sequences or random identifiers on hot paths.
- **Timestamps in UTC with microsecond precision.**
- **Reference data lives in reference tables;** other tables carry identifiers, not strings.

---

## Delivery

- CI runs the same gates for every repository: format, build, vet, lint, tests with the race
  detector, coverage floors, image size budget.
- The pipeline is the only authority on green. A local run proves nothing about the merge.
- Image size and binary size are budgeted per repository and checked on every pull request.
