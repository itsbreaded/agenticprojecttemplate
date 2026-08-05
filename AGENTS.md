# <Project>

## Project

<!-- TODO: Replace <Project> everywhere with your project name, and fill in
     a one-line description below. -->

<Project> — <one-line description of what this is>.

> Repo status: greenfield / being initialized. Update this section as the
> stack, entry points, and conventions solidify.

## Shared Agent Skills

Project skill contents live only in `.agents/skills/`. If Claude Code is used,
`.claude/skills/` is a local, uncommitted junction or symlink to that canonical
directory. Read and edit skills through `.agents/skills/<skill>/SKILL.md`; do
not create copies through the alias.

## How to document a change

Keep this file and `docs/` as a two-layer split:

- `AGENTS.md` holds concise rules a future agent must respect at decision time.
- `docs/<subsystem>.md` holds mechanism, rationale, failure modes, and other
  details needed only when touching that subsystem.
- A guardrail group ends with a link to its focused doc, and that doc names
  which `AGENTS.md` guardrails it expands. Every docs-index entry must point
  to a real file.
- Prefer a one-line rule over a doc when the lesson is self-contained. Do not
  duplicate code comments, git history, or unrelated subsystem narratives.

`## Planning Specs` is the exception: specs and their adjacent plans live in
`specs/`, not `docs/`.

## Planning Specs

Use `specs/pending/` for planned work that needs design before implementation.
Name spec files with the next unused three-digit global sequence and a
kebab-case title, checking both `specs/pending/` and `specs/done/`. Preserve
the number when moving a spec to `specs/done/`.

Specs contain WHAT/WHY: the problem, intended behavior, requirements,
scenarios, non-goals, and consequential decisions. The adjacent
`<slug>.plan.md` contains the repository-specific HOW: architecture, files,
symbols, sequencing, tasks, risks, and verification. Keep both artifacts
practical and remove stale work.

The lifecycle is:

```text
draft-spec -> brainstorm-spec -> plan-spec -> review-plan -> execute-spec -> verify-spec
```

`brainstorm-spec` makes the behavioral contract ready. `plan-spec` creates a
plan with `Plan Status: review`; `review-plan` independently approves it or
requests changes. `execute-spec` requires `Plan Status: approved` and must not
invent a minimal plan to bypass that gate. `verify-spec` records evidence and
archives only a passing spec and its plan.

### Agent workflow guardrails

- Plan approval is a technical readiness gate, not authorization for an
  unapproved product, security, privacy, cost, destructive, or external-side-
  effect decision.
- Record requirements, scenarios, non-goals, decisions, reviewer feedback,
  implementation evidence, and verification evidence in the spec or adjacent
  plan; do not make chat the only record.
- Never claim a check, review, runtime observation, or user approval that did
  not occur. Treat missing behavioral evidence as `UNVERIFIED`.
- Archive only after every applicable requirement and scenario has passing
  evidence and the spec/plan are moved together to `specs/done/`.

See [`docs/writing-specs.md`](docs/writing-specs.md) and
[`docs/writing-plans.md`](docs/writing-plans.md) for the detailed contracts.

## Docs index

`docs/` contains on-demand technical documentation. Read only the docs needed
for the current task; keep this index accurate when files are added, removed,
or materially changed.

- [`docs/README.md`](docs/README.md) — organization and read-on-demand policy.
- [`docs/writing-specs.md`](docs/writing-specs.md) — spec principles,
  scenarios, definition of done, and lifecycle.
- [`docs/writing-plans.md`](docs/writing-plans.md) — implementation-plan
  structure, review gate, task quality, and evidence loop.

## Quick start

<!-- TODO: fill in once the stack is chosen. -->
<!-- Examples:
- Language/runtime: ...
- Install: `<install command>`
- Run dev: `<development command>`
- Run tests: `<test command>`
- Lint/format: `<lint or format command>`
-->

## Project guardrails

<!-- TODO: Add terse, project-specific non-negotiables here as the project
     gains architecture and subsystem knowledge. Link mechanism docs from
     each guardrail group instead of narrating them in this file. -->
