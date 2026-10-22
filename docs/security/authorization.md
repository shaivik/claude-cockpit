---
title: Authorization
summary: Permission rules, org policy limits and file-permission hygiene governing what Claude Code may do.
sources:
  - settings.json
  - policy-limits.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Authorization

## Authorization model

Tool calls are gated by allow / ask / deny rules, then org policy limits.

## Roles / Permissions

Single user. Rules are in [settings.json](../domain/configuration/settings.md): read-only `glab` allowed, writes ask, destructive denied.

## Resource-level access

Org policy: remote control, quick web setup and web-search MCP isolation are disabled/not allowed ([managed settings](../domain/configuration/managed-settings.md)).

## Policy implementation

Enforced by Claude Code; policy files are signed.

## Admin access

Org admin controls `remote-settings*` and `policy-limits*`.

## Important authorization boundaries

- Sensitive files (mode 600): `history.jsonl`, `projects/`, `ide/`, `sessions/*.key`, `remote-settings*`, `policy-limits*`.
- Do not share or commit this directory.

## Related Documentation

- [Authentication](authentication.md)
