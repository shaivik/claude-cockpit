---
title: Backup and Restore
summary: What Claude Code backs up automatically and what you should back up yourself.
sources:
  - backups/
  - shell-snapshots/
  - docs/backups/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Backup and Restore

## Backup Strategy

| Item | Mechanism |
|---|---|
| `~/.claude.json` | Auto: `backups/.claude.json.backup.<epoch-ms>` (5 kept) |
| Edited files | Auto: `file-history/` |
| Config, skills, plans, memory | **Manual** — copy or place in a private Git repo, excluding secrets |
| Docs | The docs-generator keeps originals in `docs/backups/` when it rewrites pages |

Exclude from any backup: `history.jsonl`, `projects/`, `ide/`, `sessions/`, `remote-settings*`.

## Backup Frequency

Auto backups are created on config changes; manual — unspecified.

## Restore Procedure

Copy the chosen `backups/.claude.json.backup.<epoch-ms>` over `~/.claude.json` while Claude Code is closed.

## Related Documentation

- [Disaster recovery](disaster-recovery.md)
