---
title: Low-Level Diagram
summary: Internal module breakdown of ~/.claude by folder, including skill script layering and data flow.
sources:
  - skills/
  - plugins/
  - projects/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Low-Level Diagram

```mermaid
flowchart TD
  Prompt[User prompt] --> Hist[history.jsonl]
  Prompt --> Load["Load CLAUDE.md + settings.json + skills + memory"]
  Load --> Tool[Tool call]
  Tool --> Perm{"permissions: allow / ask / deny"}
  Perm --> HookPre[PreToolUse hook]
  HookPre --> Exec[Execute]
  Exec --> FH["file-history: snapshot per edit (hash at vN)"]
  Exec --> Tr["projects: session transcript .jsonl"]
```

## Modules

| Module | Folder |
|---|---|
| Skills | `skills/<name>/{SKILL.md, instructions.md, scripts/}` |
| Plugin store | `plugins/{cache,marketplaces,store,synced,.trash}` |
| Project state | `projects/<encoded-cwd>/{*.jsonl, <session>/, memory/}` |

## Internal components

- **Skill layering** (from [CLAUDE.md](../domain/configuration/claude-md.md)): CLI entry `scripts/<name>.py` → private helpers `scripts/_*.py` → shared infra `../../shared/` (referenced; not present at the moment).
- **Workers / Controllers / Repositories / Event handlers**: not applicable.

## Important dependencies

`uv`, Python stdlib/PyYAML, per-skill HTTP clients (`_prometheus.py`, `_tempo.py`, `_pganalyze.py`).

## Internal data flow

Config flows inward (files → Claude Code); state flows outward (Claude Code → `projects/`, `file-history/`, `telemetry/`).

## Related Documentation

- [Skills system](../domain/business-logic/skills-system.md)
- [Sessions and memory](../domain/business-logic/sessions-and-memory.md)
