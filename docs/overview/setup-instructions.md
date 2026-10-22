---
title: Setup Instructions
summary: How this directory is created, what tools skills need, and how to verify it works.
sources:
  - settings.json
  - CLAUDE.md
  - skills/docs-generator/SKILL.md
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Setup Instructions

The directory is created automatically on first run of `claude`. Setup means editing the few hand-maintained files and installing skill prerequisites.

## Prerequisites

- Claude Code installed (native installer; `.last-update-result.json` shows `path: native`).
- Signed in to the Anthropic account (creates `remote-settings*`, `policy-limits*`, `skills/synced/`).

## Required Tools

| Tool | Needed by |
|---|---|
| `uv` | all skills that run `uv run $SKILL_DIR/scripts/...` |
| `glab` | permission rules in `settings.json`, GitLab plugin |
| `~/.config/iterm2/cc-status` | every hook in `settings.json` (must exist and be executable) |
| `prettier`, `mmdc` (optional) | `docs-generator` lint |

## Repository Setup

Not applicable — not a Git repository. Back up `CLAUDE.md`, `settings.json`, `skills/` and `plans/` manually (see [backup and restore](../operations/backup-restore.md)).

## Environment Variables

| Variable | Required | Default | Purpose | Defined in |
|---|---|---|---|---|
| `OTEL_RESOURCE_ATTRIBUTES` | No | none | Tags telemetry with developer email and `team.id` | `settings.json` `env` |

Skills have their own variables/config; see [skills catalogue](../domain/workers/files/skills-catalogue.md).

## Database Setup

Not applicable — no database.

## External Dependencies

GitHub (plugin marketplace), Anthropic API, Grafana Cloud OTLP, and per-skill systems (Prometheus, Postgres, etc.).

## Running the Application

Run `claude` in any project, or use the VS Code extension. Global files load automatically.

## Running Background Workers

Not applicable. See [skills](../domain/workers/overview.md) for the closest equivalent.

## Running Tests

Only `skills/security-audit/validate-*.test.cjs` ship tests. See [testing](../guidelines/testing.md).

## Troubleshooting

| Symptom | Check |
|---|---|
| Hook errors on every event | `~/.config/iterm2/cc-status` missing or not executable |
| `/graphify` not found | `skills/graphify/` is absent; `CLAUDE.md` still references it |
| Skill script `no such file` | Use the absolute `~/.claude/skills/<name>` path; `$SKILL_DIR` is a placeholder |
| MCP tools unavailable | Authenticate servers listed in `mcp-needs-auth-cache.json` via `/mcp` |

## Related Documentation

- [Description](description.md)
- [Settings](../domain/configuration/settings.md)
