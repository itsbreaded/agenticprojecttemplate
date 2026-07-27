---
name: verify-spec
description: Independently verify a spec against its requirements and scenarios, autonomously repair unambiguous implementation gaps, record durable evidence, and archive a passing spec. Use for requests to verify, check, accept, sign off, finish, or close a spec, and for /verify-spec.
---

# verify-spec

Independently decide whether a spec is done. A passing verification is archived immediately: `brainstorm-spec -> execute-spec -> verify-spec` ends with a complete, mechanically sound, durable record.

## Invocation and gate

`/verify-spec @path/to/spec.md`. If omitted, list `review` and `in-progress` specs in `specs/pending/`.

- Refuse a spec already under `specs/done/`.
- Stop on `draft` or `ready`; send it to `execute-spec`.
- `review` is the normal handoff.
- `in-progress` is rescue verification: continue only if its plan shows every requirement task complete. Otherwise report missing work and leave it in progress.

## Preflight and independence

1. Read the spec and adjacent `specs/pending/<slug>.plan.md`; for existing work also recognize `specs/plans/<slug>.md` and migrate it beside the spec when next updating it. If no plan exists, establish relevant files from version control and record the limitation.
2. Read only applicable repository guidance. Discover runnable checks from the project's command manifest; never assume scripts exist.
3. If this session also implemented the spec, obtain an independent blind requirements/scenario pass using available delegation, or explicitly state that independence is unavailable before proceeding.
4. Treat dependency status as advisory. Confirm required behavior in code; fail only if it is unavailable or ambiguous.

## Build and run the verification matrix

For every requirement, acceptance scenario, non-goal, consequential resolved decision, and dependency, record `PASS`, `FAIL`, or `UNVERIFIED` and concrete evidence: test name, command result, or reproducible manual/code-path check. Try to falsify each item before accepting it.

An unresolved Open Question, a missing demonstration, a broken available mechanical check, or scope creep is not a pass. Run available typecheck, build, and full test commands. Run end-to-end checks when the changed surface includes user-visible app behavior, IPC, startup, or browser automation; otherwise record why they were not applicable. Inspect for debug code and dead/commented-out code.

## Repair loop

Fix an issue autonomously when the spec unambiguously defines expected behavior and the repair is minimal, idiomatic, and does not create a new visible product choice. This includes mechanical failures, missing wiring, straightforward missing tests, and stale debug code.

After each repair, run the affected check, then the full available unit suite, and re-evaluate affected matrix items. Continue while each attempt adds evidence or narrows the issue. Stop when work repeats without evidence, grows into a redesign, changes product intent, or needs a material scope, cost, security/privacy, or irreversible decision. Leave `Status: in-progress` and report that issue for `brainstorm-spec`.

## Record and decide

Append `## Verification Evidence` to the plan: requirement/scenario verdicts and evidence; non-goal/dependency checks; commands and results; deliberate exclusions or manual/runtime limits; and autonomous repairs.

When every item passes, set `Status: done`, set `Completed:` to today's date, move both spec and adjacent plan to `specs/done/`, re-read them to confirm, and report the evidence summary.

If a non-repairable gap remains, do not archive. Set `Status: in-progress`, leave evidence in pending, and state the exact decision or missing behavior.

## Guardrails

- Evidence, not opinion: no requirement passes merely because the code looks plausible.
- Do not edit requirements, scenarios, non-goals, or decisions to make a spec pass; amend those through `brainstorm-spec`.
- Archive whole specs only. A partial archive is a failure, not a shortcut.
