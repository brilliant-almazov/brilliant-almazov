# Monolith → services: the method

The starting point is a large, clean, domain-driven Symfony monolith — well-architected and
actively maintained. It is not being rescued from itself. Hot and asynchronous paths are peeled
off into Go services for **resource efficiency and independent scaling**.

This is a strangler migration with measurements at every step.

---

## Why move at all

| Cost of the framework at scale | Effect |
|---|---|
| 100+ MB bootstrap per worker (typical daemon ~150 MB resident) | the machine bill scales with worker count, not with work |
| 50–200 ms framework overhead on hot paths | internal latency and scrape cost |
| Background jobs share the HTTP bootstrap | no independent scaling of a hot path |

The monolith keeps what it is good at: the rich business UX and deeply framework-flavoured
domain models. Nothing is thrown away.

## What gets measured

| Layer | Before | After | Improvement |
|---|---|---|---|
| Resident memory per worker | 100+ MB (~150 MB typical) | ~20 MB per Go binary | ~7× |
| Container image | 100+ MB | 20–30 MB | 5–10× |
| Metrics scrape latency | 50–200 ms | sub-millisecond | 50–200× |
| New service to production | ~1 week | 1 day | ~5× |

These are differences on the same production workload, before and after each peel-off.

## How one context is peeled off

1. **Define the boundary.** What does this context own — which writes, which reads?
2. **Lock the contract.** The schema lands in the shared proto repository first; both sides get
   generated stubs.
3. **Replicate or dual-write.** Either the old side writes to both, or the new service is an
   asynchronous replica fed by an outbox and the bus — cleaner for read-heavy domains.
4. **Switch readers.** Read paths move from local tables to the contract call.
5. **Drop the old write path** once the new one is stable and back-pressure is verified.
6. **Reclaim resources.** Old workers, daemons and schemas go away.

No step moves forward until the dashboards show the new path is healthy.

## Rules learned the hard way

- **Never a big-bang rewrite.** Every step is reversible until the old path is dropped.
- **Two systems that must agree need tests that compare them,** not tests that trust one.
- **The bus is the seam.** If a context cannot be reached through events or a contract, the
  boundary is drawn in the wrong place.
- **Shared database access is not a migration step.** It is the thing being removed.
- **Measure before and after each peel-off.** A migration without numbers is a preference.
