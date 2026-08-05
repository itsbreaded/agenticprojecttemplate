# Writing good specs

Detailed guidance for authoring specs in this repository. Read this when
drafting or reviewing a spec; routine implementation work should use the
focused subsystem docs instead. Repository-wide rules and the docs map live
in [`AGENTS.md`](../AGENTS.md).

This document expands the Planning Specs and agent workflow guardrails in
`AGENTS.md`.

A copy of `specs/TEMPLATE.md` is the recommended starting point.

## Principles

Specs are the contract between intent and implementation. They keep an
autonomous agent building the right thing rather than a plausible-looking
thing. Write them to minimize ambiguity.

- **Describe behavior, not implementation.** Say what the system must do and
  why, not how to code it. "Persist user data between sessions" is a
  requirement; "use a particular database" is a plan decision.
- **One concern per spec.** Split unrelated outcomes so each spec is easier to
  review, implement, and verify.
- **Make requirements verifiable.** Every requirement should have a clear
  pass/fail test or observable check. Avoid unmeasurable words such as "fast"
  or "good" without a threshold.
- **State non-goals explicitly.** Out-of-scope behavior prevents gold-plating
  and makes verification honest.
- **Write acceptance scenarios as tests.** Given/When/Then scenarios should
  cover normal, empty, invalid, error, permission, and large-input behavior
  when relevant.
- **Capture the why.** Record the problem and consequential tradeoffs so a
  future reader can distinguish intent from an implementation detail.
- **Resolve open questions before implementation.** Ambiguity is cheaper to
  resolve in the spec than in code.
- **Keep a ready spec stable.** If intent changes materially, reopen it
  through `brainstorm-spec` or create a follow-up spec; do not silently edit
  an agreed contract during execution.

## Definition of done

A feature is not done because code exists or a broad test command is green.
The adjacent plan must be approved before implementation, implementation
tasks must record concrete checks, and `verify-spec` must map every
requirement, scenario, non-goal, decision, and dependency to `PASS`, `FAIL`,
or `UNVERIFIED` evidence. Only a complete passing matrix with applicable
checks green may move the spec and plan to `specs/done/`.

User-visible, destructive, external-side-effect, security, privacy, or costly
choices still require explicit user or maintainer authorization. Technical
plan approval is not a substitute for that product decision.
