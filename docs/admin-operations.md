# Operational control plane

> In a serious production environment engineers do not hold direct database credentials, do not
> SSH into containers and do not run ad-hoc SQL. They need a sanctioned tool. That tool is the
> control plane.

This is not an admin CRUD. It is a platform-wide operational surface with access control,
audit, safety rails and structured workflows.

---

## What it solves

| Need | How the control plane answers it |
|---|---|
| Inspect a table | Read-only browser over service databases. No client credentials handed out. |
| Change a row | A validated form with confirmation and a permanent audit record of who, what, when. |
| Undo a mistake | Soft delete is the default: the row is hidden, not gone. Hard delete is explicit and irreversible. |
| Run a maintenance job | Pre-defined, parameterised, audited operations. No bash on a laptop. |
| Understand a state | Audit log with field-level diffs and resolved references. |
| Give access safely | RBAC: the same surface, permissions scoped per role. |

## Audit is the platform's memory

Every write is recorded with field-level diffs and explicit action semantics — insert, update,
soft delete, hard delete. References are **resolved at write time**: an audit record stores not
only `some_reference_id: 129` but the resolved object as it was. A year later, after IDs have
been re-mapped or rows archived, the record still reads.

## Access control

Authentication through an external identity provider with single sign-on; authorisation in the
backend-for-frontend layer. Read-only roles for analysts, write for operators, destructive
actions for senior engineers only. Cross-origin policy, rate limiting and telemetry sit in the
gateway in front of it.

## Operations, not scripts

Maintenance work is exposed as named, parameterised, audited jobs: copying a table subset
between data sources with mapping and filtering, archiving cold rows out of hot tables,
running platform migrations, replaying a queue. Each one is repeatable, reviewable and
attributable — which is the difference between an operation and an incident waiting to happen.

## Design rules

- **Read by default, write by exception, destroy by ceremony.**
- **Every mutation is attributable.** No shared service accounts for human actions.
- **Configuration over code for presentation.** Which columns are visible, editable or
  filterable is declarative; changing it is not a deploy.
- **The control plane never becomes a second source of truth.** It operates services; it does
  not own their data.
