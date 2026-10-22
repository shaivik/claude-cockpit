---
title: Plugins and Marketplaces
summary: How plugins are installed, cached and enabled, and what is currently installed.
sources:
  - plugins/installed_plugins.json
  - plugins/known_marketplaces.json
  - settings.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Plugins and Marketplaces

## Purpose

Plugins bundle skills, MCP servers and commands from a marketplace. State lives in `plugins/`; enablement lives in `settings.json` `enabledPlugins`.

## Business Rules

| Item | Value |
|---|---|
| Marketplace | `claude-plugins-official` → GitHub `anthropics/claude-plugins-official` |
| Installed | `gitlab@claude-plugins-official` (scope `user`, commit `af59ee3a1051`) |
| Enabled | `enabledPlugins["gitlab@claude-plugins-official"] = true` |
| Cache layout | `plugins/cache/<marketplace>/<plugin>/<12-hex sha>/` (one per version; 8 gitlab versions kept) |
| Data plugins | `plugin:data:*` (amplitude, atlassian, bigquery, hex, definite) come from `plugins/synced/` |

## Workflow

`/plugin` installs → files cached → `installed_plugins.json` updated → enable flag in settings. Marketplace refreshes update `lastUpdated`.

## State Transitions

Not applicable.

## Validations

Installed path must exist; stale SHAs in `cache/` are safe to prune.

## Side Effects

Plugin MCP servers appear in `mcp-needs-auth-cache.json` until authenticated.

## Failure Handling

`plugin:data:definite` failed to connect (endpoint not found) in the latest session.

## Related Documentation

- [Settings](../configuration/settings.md)
- [Directory reference](directory-reference.md)
