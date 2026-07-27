# Agentic Project Template

A starter repository for building software with AI coding agents —
Claude Code, Codex, and similar tools — using **spec-driven development**.
Drop in your stack and start features from a spec instead of a vague prompt,
so agents build *the right thing* rather than a plausible-looking thing.

## Why

AI agents are most useful when the intent is unambiguous. This template gives
you a lightweight structure for capturing intent before code is written:

- **`AGENTS.md`** — the single canonical instructions file. Both Claude Code
  and Codex read it. It documents the project, a docs index, a quick start,
  and the spec-driven workflow.
- **`specs/`** — one Markdown file per feature. A spec describes the *what*
  and *why* (problem, goals, verifiable requirements, acceptance scenarios,
  non-goals), not the *how*. Specs move `pending/` → `done/` as they ship.
- **`docs/`** — on-demand technical documentation that is deliberately *not*
  frontloaded into agent context. Agents read a doc only when a task needs it.
- **`.agents/skills/`** — project-local skills that automate the workflow:
  - `brainstorm-spec` — flesh out a draft spec until it's ready for handoff.
  - `execute-spec` — implement a ready spec one piece at a time.
  - `verify-spec` — verify an implementation against its spec.
  - `link-claude-skills` — share one skill source between Claude Code and
    Codex, and keep `CLAUDE.md` a thin pointer to canonical `AGENTS.md`.

## The workflow

```
spec (WHAT/WHY)  →  plan (HOW)  →  implement  →  verify against spec  →  ship
```

1. **Write the spec first.** No spec = no code.
2. **Review the spec.** A spec is cheap to change; code is expensive.
3. **Plan, then implement.** Implementation details live in the plan/PR.
4. **Verify against the spec.** Done means every requirement and acceptance
   scenario is demonstrably met.
5. **Archive.** Move the spec from `specs/pending/` to `specs/done/`.

## Quick start

1. **Use this template** — click GitHub's *Use this template* button, or
   clone and re-point the remote:
   ```sh
   git clone https://github.com/itsbreaded/agenticprojecttemplate.git my-project
   cd my-project
   git remote set-url origin <your-repo-url>
   ```
2. **Edit `AGENTS.md`** — replace `<Project>` with your project name and
   description, then fill in the Quick start section once you've chosen a stack.
3. **Start a feature** — copy `specs/TEMPLATE.md` into `specs/pending/` and
   name it with the next unused three-digit number and a kebab-case slug
   (e.g. `001-add-auth.md`). See `docs/writing-specs.md` for spec principles.
4. **Link skills to your agent** — run the `link-claude-skills` skill. It
   aliases `.claude/skills` to canonical `.agents/skills` and creates a
   `CLAUDE.md` pointer to `AGENTS.md` so Claude Code and Codex share one
   source of truth.

## Requirements

- [Git](https://git-scm.com/)
- An AI coding agent that reads `AGENTS.md` (Claude Code, Codex, etc.)

Skills are plain Markdown — no runtime or package install is needed to read
them. Specific skills may invoke shell commands; see each `SKILL.md` for
details.

## Repository layout

```
.
├── AGENTS.md              # Canonical agent instructions (read by Claude Code & Codex)
├── docs/                  # On-demand technical docs (not frontloaded into context)
│   ├── README.md
│   └── writing-specs.md
├── specs/                 # Spec-driven development
│   ├── TEMPLATE.md        # Copy this to start a new spec
│   ├── pending/           # Specs not yet shipped
│   └── done/              # Shipped specs
└── .agents/skills/        # Project-local agent skills
    ├── brainstorm-spec/
    ├── execute-spec/
    ├── verify-spec/
    └── link-claude-skills/
```

## License

None yet. Add a `LICENSE` file if you intend to share or accept contributions.