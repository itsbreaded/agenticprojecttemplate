# docs/

Detailed, on-demand technical documentation. These files are **not**
frontloaded into context — they are read only when a task needs them.

Each file should be self-contained and focused on one topic. Keep the
`## Docs index` section in the root `CLAUDE.md` up to date whenever a file
is added, removed, or significantly changed, so the index stays the
accurate map of what lives here.

## Suggested organization

Group related files into subfolders as the collection grows, e.g.:

- `docs/models/` — AI model specifics (capabilities, limits, pricing,
  quirks, version notes).
- `docs/architecture/` — system design, data models, diagrams.
- `docs/integrations/` — third-party APIs, SDKs, auth flows.
- `docs/runbooks/` — operational how-tos and troubleshooting.

## When to read these files

Read on demand — only when the current task depends on them. If a file is
frequently needed, consider promoting its key facts into `CLAUDE.md`
instead of re-reading it every session.
