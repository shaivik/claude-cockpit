---
title: settings.json
summary: Every key in the user settings.json — model, env, permissions, hooks, plugins and UI — with effect.
sources:
  - settings.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# settings.json

## Configuration sources

Precedence (low → high): managed settings ([page](managed-settings.md)) override this user file for keys they set; project `.claude/settings*.json` apply per repo.

## Environment variables

| Variable | Required | Default | Purpose | Defined in |
|---|---|---|---|---|
| `OTEL_RESOURCE_ATTRIBUTES` | No | none | `developer.email=…,team.id=++` on exported telemetry | `settings.json:env` |

## Default values

| Key | Value | Effect |
|---|---|---|
| `model` | `sonnet` | Default model alias |
| `effortLevel` | `medium` | Reasoning effort |
| `tui` | `fullscreen` | Fullscreen terminal UI |
| `voice` | `{enabled: true, mode: "hold"}` | Hold-to-talk voice input |
| `switchModelsOnFlag` | `false` | Do not auto-switch models |
| `enabledPlugins` | `gitlab@claude-plugins-official: true` | Enabled plugins |

## Permissions (GitLab CLI)

| Rule set | Patterns |
|---|---|
| allow (read-only) | `glab mr list/view/diff`, `glab issue list/view`, `glab ci list/view/trace` |
| ask (writes) | `glab mr create/note/merge`, `glab issue create/note`, `glab api` |
| deny (destructive) | `glab repo delete`, `glab ci delete`, `glab mr delete`, `glab issue delete`, `glab api -X DELETE`, `glab api --method DELETE` |

Deny wins over ask/allow. Syntax: `Bash(<prefix>:*)`.

## Hooks

See [Hooks](../business-logic/hooks.md).

## Required vs optional settings

All keys optional; the file is valid JSON and Claude Code reloads it on change.

## Environment-specific / Feature flags / Third-party

Not applicable beyond the above.

## Configuration precedence

Managed > command-line > local project > project > user (this file).

## Sensitive configuration handling

The email in `OTEL_RESOURCE_ATTRIBUTES` is PII; do not commit this directory.

## Related Documentation

- [Managed settings](managed-settings.md)
- [Hooks](../business-logic/hooks.md)
