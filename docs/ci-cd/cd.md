---
title: CD
summary: Describes how changes reach effect in ~/.claude (immediately on save or via managed sync) since there is no deployment.
sources:
  - plugins/
  - skills/synced/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# CD

Not applicable — nothing is deployed. Change propagation:

| Change | Takes effect |
|---|---|
| `CLAUDE.md`, `settings.json`, `skills/<name>` | Next session (settings often live-reload) |
| Plugin install/update | Via `/plugin`; auto-update recorded in `.last-update-result.json` |
| Synced skills / managed settings | Server push at sync time |
| Claude Code version | Native auto-update (2.1.306 → 2.1.308 on 2026-10-22) |

Rollback: restore from your own copy; see [backup and restore](../operations/backup-restore.md).

## Related Documentation

- [CI](ci.md)
