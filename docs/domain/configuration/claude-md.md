---
title: CLAUDE.md
summary: Content and purpose of the global CLAUDE.md instructions file loaded in every project.
sources:
  - CLAUDE.md
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# CLAUDE.md

## Configuration sources

`~/.claude/CLAUDE.md` is loaded into every session as the user's private global instructions. Project `CLAUDE.md` files add to it.

## Current content

| Section | Effect |
|---|---|
| Skill scripts (`$SKILL_DIR`) | Explains placeholder substitution and the CLI / `_*.py` helpers / shared infra layering ([skills system](../business-logic/skills-system.md)) |

## Guidance

Keep it short; put workflows in skills rather than here.

## Related Documentation

- [Skills system](../business-logic/skills-system.md)
- [settings.json](settings.md)
