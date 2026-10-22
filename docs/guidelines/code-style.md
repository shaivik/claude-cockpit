---
title: Code Style
summary: Conventions observed for skills, scripts and config files in ~/.claude.
sources:
  - skills/
  - CLAUDE.md
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Code Style

## Language conventions

Python skill scripts launched via `uv run`; Node `.cjs` validators in `security-audit`; JSON config 2-space indented.

## Naming / Directory conventions

- Skill folder = kebab-case = frontmatter `name`.
- Entry script `scripts/<name>.py` or `scripts/<verb>_<noun>.py`; helpers `_*.py`.
- Long instructions go in `instructions.md`; `SKILL.md` stays short with trigger description.

## Error handling / Logging / Comments

Scripts print JSON to stdout for the model to read (see docs-generator). No further standard documented — see [FAQs](../references/faqs.md#open-questions).

## Linter/formatter configuration

None in this folder; docs-generator optionally runs `prettier`.

## Related Documentation

- [Skills system](../domain/business-logic/skills-system.md)
