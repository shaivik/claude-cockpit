---
title: Disaster Recovery
summary: What is lost and how to rebuild ~/.claude after deletion or corruption.
sources:
  - README.md
  - plugins/installed_plugins.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Disaster Recovery

## Recovery Objectives

No formal RPO/RTO. Irreplaceable: `CLAUDE.md`, `settings.json`, custom `skills/`, `plans/`, `projects/*/memory/`.

## Failure Scenarios

| Scenario | Impact | Recovery |
|---|---|---|
| Directory deleted | Lose config, skills, history | Re-login; restore your backup copy; reinstall plugins (`/plugin`); synced skills/policy return automatically |
| `settings.json` invalid JSON | Settings ignored | Fix JSON or restore |
| Managed file edited | Overwritten on sync | Do nothing |
| `projects/` deleted | No resume or memory | None unless backed up |

## Recovery Procedure

1. Restore backed-up files into `~/.claude/`.
2. Start `claude`, sign in.
3. Reinstall plugins listed in `plugins/installed_plugins.json`.
4. Recreate hook script `~/.config/iterm2/cc-status` (outside this folder).

## Related Documentation

- [Backup and restore](backup-restore.md)
