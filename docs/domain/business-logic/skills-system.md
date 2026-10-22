---
title: Skills System
summary: How custom skills in ~/.claude/skills are structured, discovered, invoked and how $SKILL_DIR scripts are layered.
sources:
  - CLAUDE.md
  - skills/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Skills System

## Purpose

A skill is a folder that packages a repeatable workflow. Claude Code lists each skill's `name` and `description`, and loads the full instructions only when a request matches or the user types `/<name>`.

## Business Rules

- Folder pattern: `skills/<kebab-name>/` with required `SKILL.md` (YAML frontmatter `name`, `description`).
- Optional files: `instructions.md` (step-by-step), `references/`, `scripts/`, config (`queries.yaml`), notes.
- `description` doubles as the trigger text; write it with explicit "Trigger when…" phrasing.
- `$SKILL_DIR` in instructions → `~/.claude/skills/<name>` (substitute before running `uv run $SKILL_DIR/...`).
- Script layers: CLI entry (`scripts/<name>.py`), private helpers (`scripts/_*.py`), shared infra (`../../shared/`, not currently present).
- `skills/synced/<org>_<acct>/` is server-managed; do not hand-edit.

## Workflow

1. User types `/skill-name` or a matching request.
2. Claude reads `SKILL.md`, then `instructions.md`.
3. Runs the CLI script, interprets JSON output, produces report.

## State Transitions

Not applicable.

## Validations

`skill-creator` (synced) has `quick_validate.py`. The empty `anatomy/` folder noted in README no longer exists.

## Side Effects

Scripts may call external systems (Prometheus, Postgres, SSH). Check each skill page for write behaviour.

## Failure Handling

`CLAUDE.md` references `/graphify` but `skills/graphify/` is missing; the invocation will fail until reinstalled.

## Related APIs / Models / Workers

- [Skills catalogue](../workers/files/skills-catalogue.md)

## Related Documentation

- [CLAUDE.md](../configuration/claude-md.md)
- [Directory reference](directory-reference.md)
