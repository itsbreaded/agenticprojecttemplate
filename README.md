# Agentic Project Template

A starter repository for building software with AI coding agents using
spec-driven development. Drop in your stack and start features from a spec
instead of a vague prompt, so agents build the intended behavior.

## Why

This template provides a lightweight structure for capturing intent before
code is written:

- **AGENTS.md** is the canonical project instruction file.
- **specs/** holds one behavioral contract per feature.
- **docs/** holds focused, on-demand technical documentation.
- **.agents/skills/** holds the workflow skills shared by Codex and Claude
  Code.

The workflow skills are:

- `draft-spec` - research an idea into a pending spec draft.
- `brainstorm-spec` - refine a draft until its requirements are ready.
- `plan-spec` - write a detailed implementation plan.
- `review-plan` - independently review and approve the plan.
- `execute-spec` - implement from the approved plan.
- `verify-spec` - verify the implementation and archive passing work.
- `auto-orchestrator-spec` - process the pending queue with bounded retries.
- `link-claude-skills` - share one canonical skill source between Claude Code
  and Codex.

## Workflow

```text
draft -> brainstorm -> plan -> review-plan -> execute -> verify -> archive
```

Execution requires an adjacent plan with `Plan Status: approved`. The
auto-orchestrator follows the same gates and keeps a transient checkpoint at
`specs/.auto-orchestrator-state.md`.

1. Write the spec first. No spec means no code.
2. Refine the WHAT/WHY until requirements and scenarios are verifiable.
3. Create and independently review the repository-specific HOW plan.
4. Implement only from the approved plan.
5. Verify every requirement and scenario with concrete evidence.
6. Move the passing spec and plan from `pending/` to `done/`.

## Quick start

1. Use this template or clone it into a new project.
2. Edit `AGENTS.md`: replace `<Project>`, describe the stack, and fill in
   Quick start and project guardrails.
3. Start a feature with `/draft-spec <your idea>`.
4. Link skills with `/link-claude-skills` when Claude Code is part of the
   workflow.

## Requirements

- Git
- An AI coding agent that reads `AGENTS.md`

Skills are plain Markdown; no package installation is required to read them.
Individual skills may invoke commands from the project stack.

## Repository layout

```text
.
|-- AGENTS.md
|-- README.md
|-- docs/
|   |-- README.md
|   |-- writing-specs.md
|   `-- writing-plans.md
|-- specs/
|   |-- TEMPLATE.md
|   |-- pending/
|   `-- done/
`-- .agents/skills/
    |-- brainstorm-spec/
    |-- draft-spec/
    |-- plan-spec/
    |-- review-plan/
    |-- execute-spec/
    |-- verify-spec/
    |-- auto-orchestrator-spec/
    `-- link-claude-skills/
```

Each skill folder holds a `SKILL.md`. Skills exposed as Codex agents may also
carry an `agents/openai.yaml` interface file.

## License

None yet. Add a `LICENSE` file if you intend to share or accept contributions.
