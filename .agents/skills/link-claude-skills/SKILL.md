---
name: link-claude-skills
description: Configure one project-local skill source for Codex and Claude Code by making `.claude/skills` point to canonical `.agents/skills`, and keep `CLAUDE.md` a thin pointer to canonical `AGENTS.md`. Use when asked to share, link, alias, sync, migrate, or avoid duplicating project skills or agent instructions between `.agents` and `.claude` on Windows, macOS, or Linux.
---

# Link Claude Skills

Maintain project skill contents only in `.agents/skills`. Make `.claude/skills` a local filesystem alias to that directory so Claude Code and Codex discover the same skills without copied files. Keep agent instructions canonical in `AGENTS.md` and let `CLAUDE.md` redirect Claude Code to it, so the two tools share one source of truth.

## Scope and safety

- Work from the Git repository root. If the current directory is inside a repository, find the root with `git rev-parse --show-toplevel` and use that path for every operation.
- Treat `.agents/skills` as canonical. Never edit skills through `.claude/skills`; always edit their `.agents/skills` paths.
- Do not delete, overwrite, or silently move an existing real `.claude/skills` directory. Report the conflict and ask before migrating its contents or replacing it with an alias.
- Do not commit the alias. A Windows junction is not portable through Git, and a Unix symlink can fail on Windows clones. Keep canonical `.agents/skills` under version control and create the alias locally.

## Setup

1. Confirm `.agents/skills` exists. Create it if this is a new skill setup.
2. Inspect `.claude/skills` before changing it.
   - If it already resolves to `.agents/skills`, report success and validate it.
   - If it is a real directory or points elsewhere, stop and explain the conflict. Do not replace it without explicit approval.
   - If absent, create `.claude` and make the alias for the current platform.
3. Ensure `AGENTS.md` is the canonical instructions file and `CLAUDE.md` is a thin pointer to it.
   - Canonical agent instructions (project description, docs index, quick start, spec-driven workflow) live in `AGENTS.md` at the repository root. Treat `AGENTS.md` as the source of truth; edit it directly.
   - If `CLAUDE.md` does not exist, or exists but does not point at `AGENTS.md`, (re)create it with the pointer content below. If a `CLAUDE.md` already exists with substantial, non-pointer content, stop and ask before overwriting it — the user may want that content migrated into `AGENTS.md` first.
   - `CLAUDE.md` pointer content (exact):
     ```markdown
     # Claude Code instructions

     This project keeps all agent instructions in a single canonical file:
     **`AGENTS.md`**.

     Read `AGENTS.md` and follow it. It is the source of truth for the
     project description, docs index, quick start, and spec-driven
     development workflow.
     ```
   - Commit both `AGENTS.md` and `CLAUDE.md`. The pointer is portable plain text, unlike the `.claude/skills` alias, so it belongs under version control.
4. Validate the alias and show canonical skill entries visible through it.
5. Tell the user to restart a running Claude Code session if this created its first `.claude/skills` directory. Start a new Codex session if skill discovery already occurred.

## Platform commands

### Windows PowerShell

Use a directory junction. Resolve absolute paths so the target is correct even from a nested directory.

```powershell
$root = git rev-parse --show-toplevel
$canonical = Join-Path $root '.agents\skills'
$claudeDir = Join-Path $root '.claude'
$link = Join-Path $claudeDir 'skills'

New-Item -ItemType Directory -Force $canonical, $claudeDir | Out-Null
New-Item -ItemType Junction -Path $link -Target $canonical | Out-Null
Get-Item $link | Select-Object FullName, LinkType, Target
Get-ChildItem $link -Directory | Select-Object -ExpandProperty Name
```

Do not run the junction command until inspection confirms that `$link` does not already exist.

### macOS and Linux

Use a relative directory symlink from the repository root.

```sh
mkdir -p .agents/skills .claude
ln -s ../.agents/skills .claude/skills
readlink .claude/skills
find -L .claude/skills -mindepth 1 -maxdepth 1 -type d -print
```

Do not run `ln -s` until inspection confirms `.claude/skills` does not already exist.

## Validate

- Check expected `SKILL.md` files under `.agents/skills`.
- Check the same entries are visible through `.claude/skills`.
- Confirm the alias targets the canonical path, not a copied directory.
- Confirm `CLAUDE.md` exists at the root and points to `AGENTS.md` (and that `AGENTS.md` holds the real instructions).
- Run `git status --short`; canonical skill content belongs under `.agents/skills`, while the local alias must not appear as a file tree to commit. `AGENTS.md` and `CLAUDE.md` should be tracked.

## Migration, only with approval

If an existing `.claude/skills` directory contains skills not already under `.agents/skills`, compare contents, resolve name conflicts with the user, move agreed canonical copies to `.agents/skills`, verify them, then replace the empty `.claude/skills` directory with the platform alias. Never choose a winner for conflicting `SKILL.md` files without asking.
