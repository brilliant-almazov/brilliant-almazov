# AI-augmented engineering

> The team is small. The team is AI-first. The bar is high.
>
> This document is how we keep velocity without letting AI-generated noise erode the codebase.

---

## The honest thesis on AI in engineering

> **AI helps good engineers ship faster. It helps bad engineers ship bad code faster.**

That's it. That's the whole thing. The tool is a multiplier, and it multiplies what's already there — judgement, taste, discipline, intent.

- A senior engineer with AI ships in a day what used to take a week, **and** the code passes review, **and** the tests are real, **and** the abstractions are sound — because the engineer still owns every decision, the AI just types faster.
- A junior engineer with AI ships ten times as much code in the same week, **and** every other line is subtly wrong, plausibly named, statistically correct and semantically broken — because nobody asked "does this actually fit the architecture?".

So I treat AI exactly the way I treat any other power tool: **respect the blade, build the jig, follow the standard work**. In practice that means:

- The engineer architects, decides, and reviews. The AI executes.
- Conventions live in `CLAUDE.md` and in hooks, not in the engineer's head and not in the AI's training set.
- Every change runs the same lint / type-check / unit / integration / metric gate. CI doesn't care who typed the code.
- When the AI drifts (and it will), the failure shows up in the per-task budget log, and the convention gets tightened — not the failure papered over.

Used carefully, AI is the biggest force multiplier of the last decade. Used carelessly, it's the fastest way to ship a year of technical debt in a quarter. The difference is not the model. The difference is the discipline around it.

---

## What "AI-first" actually means here

It does **not** mean "an LLM autocompletes code and we ship it". It means a deeply integrated, **disciplined** workflow where Claude Code (Opus / Sonnet), custom skills, hooks and sub-agents are part of the daily engineering loop — and the codebase still passes the same quality bar as if every line were hand-written. Often higher, because rules are enforced by hooks instead of by hope.

The leverage is real. The discipline is real too.

---

## The stack on top of the stack

| Layer | What it is |
|---|---|
| **Claude Code (Opus / Sonnet)** | The primary coding partner. Used across every active repository. |
| **Per-repo `CLAUDE.md`** | A long, prescriptive document inside every repo describing its conventions, layout, taboos and idioms. New agent sessions pick up context in one read. |
| **Custom skills** | Reusable, codified workflows for the operations done constantly: schema migrations, service scaffolding, code review, CI debugging, observability rollouts, PR generation, Linear status sync, refactor recipes, screenshot capture, deploy planning. Each skill is a self-contained markdown document that the AI invokes by name. |
| **Custom hooks** | `PreToolUse` / `PostToolUse` / `SessionStart` shell hooks that enforce conventions automatically: read-before-edit, no `chore:` commits, no AI attribution in commits, Linear assignee discipline, branch naming, no direct master push. AI cannot bypass them — the tool layer rejects the operation. |
| **Structured persistent memory** | A Markdown memory index per project: user role, feedback rules, project context, references. The agent recalls it across sessions; nothing is re-explained twice. Corrections become permanent the moment they're given. |
| **Custom sub-agents** | Focused agents (`explore`, `code-reviewer`, `test-writer`, `doc-writer`, `debug`, `security-audit`, …) dispatched in parallel for independent work, each with a strict input / output contract. Long research tasks are delegated to sub-agents so the main context stays clean. |

---

## How the discipline works

AI gives velocity. Discipline keeps it from rotting:

- **Code is reviewed and refined by hand before every commit.** AI doesn't merge anything. Nothing reaches `master` without a human PR review.
- **No throwaway AI code.** Every change passes the same lint, type-check, unit-test and integration-test gates as hand-written code. CI is the final word.
- **One struct per file, interface-driven Go, no procedural helpers, no hardcoded defaults in shared libraries.** Codified in `CLAUDE.md` and enforced by hooks — AI never gets to drift toward "let me write a quick `utils.go`".
- **`errors.Is` / `errors.As` only**, never direct comparison or type switch. Hooks reject violating code before it lands.
- **Forward-only migrations, Snowflake IDs everywhere, `COMMENT ON COLUMN` required.** Migration linting blocks anything else.
- **Real integration tests against real Postgres / NATS / RabbitMQ** in `testcontainers-go`. AI cannot fake an integration test green — the container is real.
- **Per-task Linear tracking.** Every task records its budget (time, tokens, money, ops), incidents (Claude mistakes, scope changes, spec ambiguity, tech surprises) and estimate-vs-actual. Patterns where the AI breaks the rules become **visible** — and feed back into stricter `CLAUDE.md` rules and tighter hooks.
- **No AI attribution.** Commits do not say `Co-Authored-By: Claude`. The code is the engineer's responsibility, not the model's.

---

## Productivity metrics

**Period:** Dec 2025 → Jun 2026 — about 6.5 months, 196 days.

| Metric | Value |
|---|---|
| 🗂 Active repositories | **22** (PHP, Go, Rust, TypeScript, SQL, Proto, IaC) |
| 📝 Commits authored | **6,300+** |
| ➕ Lines added (source only — excludes vendor / generated / lockfiles) | **~3,400,000** |
| ➖ Lines removed | **~1,080,000** |
| ⏱ Average commit cadence | **~32 commits / day** |
| ⏱ Average code throughput | **~17,000 lines / day** |
| 🚀 Bounded contexts extracted from the PHP monolith into Go | **6** (each running as one or more Go microservices — server, worker, sometimes more) |
| 📦 Public OSS libraries shipped | **3** (1 Go, 2 Rust) |

> Numbers are filtered to source files only (`.go .rs .php .ts .tsx .sql .proto .py .yaml .md`) and exclude `vendor/`, `node_modules/`, `.next/`, generated proto, lockfiles. They count my own commits across the existing PHP / Symfony monolith *and* the new Go / Rust platform — both are clean, actively-maintained codebases while migration is in flight.

### Per-repo activity (top 9 by commits)

| Domain | Commits | Lines (+/−) | Stack |
|---|---:|---:|---|
| PHP / Symfony monolith (clean, domain-driven; partial migration in flight) | **2,806** | +2,020k / −780k | PHP · Symfony · MySQL · Redis · RabbitMQ |
| Provider execution arm | 1,416 | +493k / −139k | Go · NATS · gRPC · Postgres |
| Admin & operational control plane | 825 | +404k / −72k | Go BFF · React · Mantine · Refine |
| Platform foundation (lib + sidecar + registry) | 394 | +197k / −15k | Go · Rust |
| Domain rule map | 275 | +69k / −28k | Go · gRPC · NATS · Postgres |
| DevOps / IaC | 124 | infra-as-code | Shell · YAML · Grafana · Prometheus |
| PHP-monolith Go runner | 99 | +35k / −10k | Go (sidecar of PHP) |
| Shared schema repo | 93 | +29k / −5k | Protocol Buffers |
| Content scraper | 92 | +60k / −20k | Go · NATS · R2 · gRPC |

These are real commits in real repos shipping real production code. No demo projects, no padding.

---

## Why it works at this scale

The honest answer: **rules enforced by tooling, not by goodwill.**

- A hook rejects a commit that violates the code style. The AI's "this is close enough" doesn't get past the gate.
- A skill encodes the *exact* steps for an operation we do twenty times a month. The AI follows the recipe; it doesn't reinvent.
- A `CLAUDE.md` describes the project's taboos. The AI reads it in every session; nothing gets re-litigated.
- The Linear budget tracking surfaces *where* the AI burns time, tokens and money — so we know which prompts to tighten and which skills to add.

The result is a team that ships at the volume of a much larger team, on a codebase that still passes a senior code review.

---

## What I learned

- **AI velocity without discipline produces unmaintainable code.** Discipline is the prerequisite, not the brake.
- **The model is best at execution, not judgement.** Every architectural decision goes through me. The model writes the code that implements the decision.
- **Conventions belong in tooling, not in your head.** The longer the project runs, the truer this gets. Hooks and `CLAUDE.md` are the institutional memory.
- **Per-task budgets matter.** Without measuring tokens / money / ops per task, you don't notice the prompts that are silently 10× more expensive than they should be.
