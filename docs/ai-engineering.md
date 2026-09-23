# AI-augmented engineering

> A small team, an AI-first workflow, and a quality bar that does not move.
>
> This document is how velocity is kept without letting generated noise erode the codebase.

---

## The honest thesis

> **AI helps good engineers ship faster. It helps bad engineers ship bad code faster.**

The tool is a multiplier, and it multiplies what is already there — judgement, taste,
discipline, intent.

- A senior engineer with AI ships in a day what used to take a week, **and** the change passes
  review, **and** the tests are real, **and** the abstractions hold — because the engineer still
  owns every decision.
- A junior engineer with AI ships ten times the code, and every other line is plausibly named,
  statistically correct and semantically wrong — because nobody asked whether it fits the
  architecture.

So I treat it like any other power tool: respect the blade, build the jig, follow the standard
work.

---

## What "AI-first" means here

Not "a model autocompletes and we ship it". It means a disciplined loop where agents, codified
skills and enforcement hooks are part of daily engineering, and the codebase passes the same
bar as if every line were hand-written — often a higher one, because the rules are enforced by
tooling instead of by hope.

| Layer | What it is |
|---|---|
| **Coding agents** | The primary implementation partner, used across every active repository. |
| **Per-repository convention file** | A long, prescriptive document describing layout, idioms and taboos. A new session picks up the context in one read. |
| **Codified skills** | Reusable recipes for the operations done constantly: migrations, service scaffolding, review, CI debugging, observability rollout. The agent follows the recipe instead of reinventing it. |
| **Enforcement hooks** | Pre- and post-tool hooks that reject a violating operation at the tool layer: read-before-edit, commit conventions, branch naming, no direct push to the protected branch. The agent cannot argue with them. |
| **Persistent memory** | A structured index of corrections and project context, so nothing is re-explained twice. |
| **Focused sub-agents** | Narrow agents with a strict input/output contract, dispatched for independent work so the main context stays clean. |

---

## The gates

- **Architecture decisions stay human.** The model executes a decision; it does not make one.
- **No standing production access for agents.** Access is granted deliberately, per task, only
  when it is needed, and it ends with the task.
- **Critical operations stay hands-on** — on purpose. Judgement stays sharp only if it is used.
- **Nothing merges without a human review.** CI does not care who typed the code, and neither
  does the reviewer.
- **The same gates as hand-written code:** format, build, vet, lint, tests with the race
  detector, coverage floors, integration tests on real infrastructure.
- **Integration tests cannot be faked green** — the database and the broker are real
  containers.
- **Conventions live in tooling, not in a head.** When an agent drifts, the rule gets tighter,
  the hook gets stricter, and the drift stops being possible.

---

## What I learned

- **Velocity without discipline produces unmaintainable code.** Discipline is the prerequisite,
  not the brake.
- **The model is good at execution, not at judgement.** Architecture goes through a person.
- **Conventions belong in tooling.** The longer a project runs, the truer that gets: hooks and
  convention files are the institutional memory.
- **Measure the loop, not the output.** Where a workflow is expensive, the fix is a tighter
  prompt or a new skill — not more output.
