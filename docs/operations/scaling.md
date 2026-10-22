---
title: Scaling and Cleanup
summary: Which folders grow over time, their current size, and safe pruning commands.
sources:
  - projects/
  - file-history/
  - plugins/cache/
  - .last-cleanup
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Scaling and Cleanup

## Scaling Strategy

Not applicable (single user); the concern is disk growth. Claude Code runs its own cleanup (`.last-cleanup` stores the last run).

## Bottlenecks

| Folder | Size (2026-10-22) | Growth driver |
|---|---|---|
| `projects/` | ~226 MB | transcripts, subagent logs, tool-results |
| `plugins/` | ~18 MB | one cache folder per plugin version |
| `skills/` | ~7 MB | model artefacts, synced skills |
| `file-history/` | ~3.9 MB | snapshots per edit |

## Capacity Planning

Prune quarterly. Safe: `cache/`, `shell-snapshots/`, `telemetry/`, `downloads/`, old `session-env/`, stale `plugins/cache/<m>/<p>/<old-sha>`, old `file-history/<uuid>`. With care: `projects/`, `history.jsonl`, `sessions/`.

## Related Documentation

- [Directory reference](../domain/business-logic/directory-reference.md)
