# Writing implementation plans

Implementation plans are the developer-facing HOW document for a ready spec.
They sit beside the spec at `specs/pending/<slug>.plan.md` and are reviewed
independently before `execute-spec` changes code. Repository entry-point rules
and the docs map are in [`AGENTS.md`](../AGENTS.md).

This document expands the Planning Specs and agent workflow guardrails in
`AGENTS.md`.

The spec remains the behavioral contract: WHAT the system does, WHY it matters,
requirements, scenarios, non-goals, and consequential decisions. The plan
contains repository-specific HOW: current code paths, boundaries, files,
symbols, sequencing, tests, risks, and implementation choices. Do not move
product intent into the plan or repeat the whole spec there.

## Lifecycle

```text
brainstorm-spec (ready)
  -> plan-spec (Plan Status: review)
  -> review-plan (approved or changes-requested)
  -> execute-spec (in-progress, then completed)
  -> verify-spec (evidence and archive)
```

`plan-spec` owns plan creation and revision. `review-plan` is the independent
pre-execution gate. `execute-spec` consumes an approved plan and may update
task status and implementation evidence, but it must not silently replace a
missing or rejected plan with a minimal one.

`Plan Status` is a state machine, not a claim of feature completion:

- `review`: plan author finished; blind review is required.
- `changes-requested`: reviewer found a gap; return to `plan-spec`.
- `approved`: reviewer found no blocking gap; execution may begin.
- `in-progress`: executor is working from the approved plan.
- `completed`: executor finished its tasks and handoff checks; verification is
  still required.

After approval, a change to scope, requirements, sequencing, invariants, or
verification strategy invalidates approval and must return the plan to
`review`. Routine task-status and evidence updates do not reopen it. Plan
review is a technical gate; it does not authorize consequential product,
security, privacy, cost, destructive, or external-side-effect decisions.

## Required shape

Use these headings unless a smaller plan genuinely makes one unnecessary:

```markdown
# Implementation Plan: <title>

Plan Status: review <!-- review | changes-requested | approved | in-progress | completed -->
Source spec: `specs/pending/<slug>.md` (Status: ready)

## Verified Repository Facts

## Scope and Coverage

| Requirement/scenario | Planned task(s) | Verification |
| --- | --- | --- |

## Architecture and Data Flow

## Implementation Tasks

### T1 - <right-sized objective> (pending)

- Dependencies:
- Requirements/scenarios:
- Files and symbols:
- Current behavior:
- Implementation change:
- Invariants and edge cases:
- Verification:
- Completion evidence:

## Cross-Cutting Constraints

## Risks, Migration, and Rollback

## Handoff Checklist

## Plan Review

## Implementation Summary

## Verification Evidence
```

The last two sections are completed during execution and verification; they
may initially say `Not started.` and contain no invented evidence.

## Task quality

Each task should be a coherent change a developer can implement and check in
one pass. Name exact files and symbols or code boundaries, not just folders.
Explain current behavior, intended change, architecture fit, and what must
remain unchanged. Map every task to requirement/scenario IDs and name the
test, assertion, command, or manual path that proves it.

Use explicit ordering when work has dependencies: data model before callers,
backend/API before UI, wiring before end-to-end checks. Call out ordering
hazards, state transitions, retries, cleanup, persistence, compatibility,
failure behavior, limits, and rollback instead of leaving them for discovery.

Avoid both extremes: a plan is not a vague checklist and not line-by-line
pseudocode. Include enough mechanism detail to make implementation predictable
and reviewable while leaving ordinary coding syntax to the implementer.

## Review checklist

The blind reviewer should be able to answer yes to all of these:

- Does every requirement and acceptance scenario have concrete coverage?
- Are proposed files, symbols, boundaries, and current-behavior claims real?
- Could a developer implement the behavior without a new product decision or
  rediscovering the architecture?
- Are sequencing, state transitions, errors, empty states, races, limits,
  cleanup, compatibility, and rollback addressed where relevant?
- Does every task have meaningful isolated verification?
- Are non-goals, risks, migration/rollback, and manual limits explicit?
- Is the plan concise, non-duplicative, and free of speculative scope?

Approval is not a code review and is not evidence that the feature works; it
only means the implementation plan is ready to execute.

## Feedback and evidence loop

Record user feedback, reviewer findings, failed checks, and runtime failures in
the durable spec/plan/evidence or a focused follow-up artifact. Prefer evidence
from the real workflow or a representative environment; structural inspection
may support a wiring claim but cannot replace a behavioral check.
