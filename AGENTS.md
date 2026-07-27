# <Project>

## Project

<!-- TODO: Replace <Project> everywhere with your project name, and fill in
     a one-line description below. -->

<Project> — <one-line description of what this is>.

> Repo status: greenfield / being initialized. Update this section as the
> stack, entry points, and conventions solidify.

## Docs index

`docs/` holds detailed, on-demand technical documentation — AI model
specifics, deeper architecture, integration details, runbooks. **These
files are not frontloaded into context.** Read a doc only when the current
task depends on it; do not read them preemptively.

When you add, remove, or materially change a doc, keep this index up to
date so it stays an accurate map of `docs/`. Each entry is one line:
`path` — what it covers / when to read it.

<!-- Add entries below as docs are created. Example:
- `docs/models/sonnet-notes.md` — Sonnet quirks, limits, pricing; read before tuning model selection or prompts.
- `docs/architecture/data-model.md` — DB schema and entity relationships; read before touching persistence.
-->

- `docs/README.md` — how the `docs/` folder is organized and when to read these files.
- `docs/writing-specs.md` — detailed spec-writing principles; read when drafting or reviewing a spec.

## Quick start

<!-- TODO: fill in once the stack is chosen. -->
<!-- Examples:
- Language/runtime: ...
- Install: `npm install` / `pip install -r requirements.txt`
- Run dev: `npm run dev`
- Run tests: `npm test`
- Lint/format: `npm run lint`
-->

## Spec-driven development (how we build features here)

This repo follows **spec-driven development**. A feature is not "done"
because the code looks right — it is done when the agreed spec is met.

### Workflow

```
spec (WHAT/WHY)  →  plan (HOW)  →  implement  →  verify against spec  →  ship
```

The skills in `.agents/skills/` automate these steps:
`draft-spec` → `brainstorm-spec` → `execute-spec` → `verify-spec`.

1. **Write the spec first.** Before any code, capture the problem, goals,
   requirements, and acceptance criteria. No spec = no code.
2. **Review the spec.** A spec is cheap to change; code is expensive. Get
   the WHAT and WHY right before writing HOW.
3. **Plan, then implement.** Once the spec is approved, design the
   implementation against it. Implementation details (files, functions,
   libraries) live in the plan/PR, not the spec.
4. **Verify against the spec.** Implementation is complete only when every
   requirement and acceptance scenario is demonstrably met.
5. **Archive.** Move the spec from `pending/` to `done/` once shipped.

### Spec folders

- `specs/pending/` — specs not yet shipped (draft, ready, in-progress, review).
- `specs/done/` — shipped specs, moved here on completion.
- `specs/TEMPLATE.md` — copy this to start a new spec.

Each spec is one Markdown file, named with the next unused three-digit global
sequence and a kebab-case slug, e.g. `053-add-user-login.md`. Check both
`specs/pending/` and `specs/done/` before choosing the number, and preserve it
when archiving. The slug is the stable identity: **cross-references between
specs, plans, and PRs use the slug, never the number**.
Creation date is recorded inside the file (`Created:` field), not in the
filename.

### Lifecycle of a spec

- **draft** — being written; requirements still in flux.
- **ready** — requirements and acceptance criteria are complete and agreed;
  implementation can begin.
- **in-progress** — being implemented.
- **review** — implementation complete, being verified against the spec.
- **done** — shipped; the file is moved to `specs/done/`.

When a spec moves to `done`, add a `Completed:` date at the top and move
the file from `specs/pending/` to `specs/done/`. Keep its filename stable
so it's easy to reference later.

### Writing good specs

Detailed spec-writing guidance (behavior over implementation, verifiable
requirements, explicit Non-Goals, Given/When/Then scenarios, capturing the
why) lives in **`docs/writing-specs.md`** — read it when drafting or
reviewing a spec. Start from `specs/TEMPLATE.md`.

### Definition of done

A spec is `done` only when ALL of these are true:

- Every requirement is met and demonstrable.
- Every acceptance scenario passes (ideally as an automated test).
- No Open Questions remain unresolved.
- The spec file is moved to `specs/done/` with a `Completed:` date.
