---
name: execute-spec
description: Implement a ready spec with a durable adjacent plan, incremental checks, and a review-ready handoff. Use for requests to implement, build, execute, or work on a spec, and for /execute-spec.
---

# execute-spec

Implement a `ready` spec and leave it at `review` for independent verification. This is the coding leg of `brainstorm-spec -> execute-spec -> verify-spec`; it does not archive the spec.

## Invocation and gate

`/execute-spec @path/to/spec.md`. If omitted, list `ready` or `in-progress` specs in `specs/pending/`.

- Refuse specs in `specs/done/`.
- Stop on `draft`; send it to `brainstorm-spec`.
- Stop on `review`; it is awaiting `verify-spec`.
- Accept `ready` and `in-progress`. Resume from adjacent `<slug>.plan.md`; for existing work also recognize `specs/plans/<slug>.md` and migrate it beside the spec when next updating it. If no plan exists, reconstruct a minimal plan from the spec and relevant diff before changing code.

## Preflight

1. Read the spec, relevant repository guidance, and cited dependencies.
2. Locate only docs relevant to the affected subsystem; do not assume generic architecture/data-source documents exist.
3. Inspect code paths the spec relies on before planning.
4. Read the project's command manifest and use only scripts that actually exist. Run typecheck, build, and tests when available; run end-to-end tests when the spec changes user-visible app behavior, IPC, startup, or browser automation.

## Create one durable plan

Create `specs/pending/<slug>.plan.md` beside the spec. It is the sole required resume and audit artifact; use transient task tooling only if it helps the current session.

For each right-sized task record status, requirement/scenario mapping, likely files or subsystem, and one isolated verification method. Every requirement needs a task; drop tasks with no requirement and split tasks covering more than three requirements. Set `Status: in-progress` once the plan exists.

## Implement

- Work in dependency order and match surrounding conventions.
- Keep each change tied to a requirement or essential implementation need.
- Run focused tests after each coherent change. Run project-wide typecheck after shared type/API changes and at handoff; do not repeat it mechanically after every small task.
- Respect non-goals and reuse existing services or boundaries where specified.
- Resolve ordinary technical details autonomously using the least-surprising, idiomatic approach.

If the spec is impossible, contradictory, or needs a genuine product, scope, security/privacy, cost, or irreversible decision, stop and report it for `brainstorm-spec`. For a missing or stale dependency, verify the behavior in code; block only when unavailable or ambiguous.

## Self-check and handoff

Run the available typecheck, build, and full test commands. Run end-to-end checks when required by the preflight impact rule; otherwise state why they were not applicable. Remove debug code and update the plan. Append `## Implementation Summary` with requirements covered, checks run, and manual/runtime limits.

On success set `Status: review` and leave `Completed:` blank. On a genuine blocker leave `in-progress` and report the precise decision or missing behavior.

## Guardrails

- The spec is read-only during execution except for `Status:`.
- Keep implementation detail in the adjacent plan, not the spec.
- `review` means implemented and mechanically checked, not archived or done.
