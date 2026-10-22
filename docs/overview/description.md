---
title: Description
summary: What the ~/.claude directory is, what lives in each subfolder, and who owns it.
sources:
  - README.md
  - CLAUDE.md
  - settings.json
  - skills/
  - plugins/installed_plugins.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Description

`~/.claude` is the per-user home of Claude Code. It holds **configuration you edit**, **extensions you install** and **state Claude Code writes while running**. It is not a service or a Git repository (`.git` absent), so there is no deploy pipeline or API.

## Purpose

- Apply the same instructions, permissions, hooks and skills in every project on this machine.
- Persist session transcripts, memory, file snapshots and caches so sessions can be resumed or rewound.

## Business Context

Used by an EatClub ops-tech engineer (`team.id=ops-tech`, see [settings](../domain/configuration/settings.md)). Custom skills target EatClub systems: Rails/Sidekiq services, Postgres, Prometheus/Tempo/pganalyze, outlet PCs and the iOS app.

## Responsibilities

- Define global behaviour: [CLAUDE.md](../domain/configuration/claude-md.md), [settings.json](../domain/configuration/settings.md).
- Host custom [skills](../domain/business-logic/skills-system.md) and installed [plugins](../domain/business-logic/plugins.md).
- Store [session transcripts and memory](../domain/business-logic/sessions-and-memory.md).

## Non-Responsibilities

- Project-specific config (lives in each repo's `.claude/`).
- Org policy authoring (pushed from Anthropic/org admin, see [managed settings](../domain/configuration/managed-settings.md)).

## Key Capabilities

| Capability | Where |
|---|---|
| Global instructions | `CLAUDE.md` |
| Settings, permissions, hooks | `settings.json` |
| Custom workflows | `skills/<name>/SKILL.md` |
| Plugin install/marketplace | `plugins/` |
| Resume / rewind | `projects/`, `file-history/` |

## Technology Stack

| Layer | Technology |
|---|---|
| Runtime | Claude Code 2.1.308 (CLI + `claude-vscode`), default model `sonnet`, effort `medium` |
| Skill scripts | Python run with `uv run`; a few Node `.cjs` validators in `skills/security-audit/` |
| State formats | JSON, JSONL, plain text/markdown, shell snapshots |
| Hooks | Shell command `~/.config/iterm2/cc-status` |

## Dependencies

### Upstream Dependencies

- Anthropic account and org (managed settings, policy limits, synced skills/plugins).
- GitHub `anthropics/claude-plugins-official` marketplace.

### Downstream Dependencies

- Grafana Cloud OTLP gateway (telemetry export, see [telemetry](../observability/telemetry.md)).
- Skill targets: Prometheus, Tempo, pganalyze, Postgres, outlet PCs over SSH/Ansible.

## Repository Structure

| Path | Kind | Usage |
|---|---|---|
| `CLAUDE.md`, `settings.json` | You edit | Global config |
| `skills/`, `plans/` | You edit | Skills and saved plans |
| `plugins/` | Managed | Plugins and marketplaces |
| `projects/`, `history.jsonl`, `sessions/`, `session-env/`, `file-history/` | Generated | Session state |
| `cache/`, `shell-snapshots/`, `telemetry/`, `debug/`, `downloads/`, `backups/`, `ide/`, `state/` | Generated | Caches and housekeeping |
| `remote-settings*`, `policy-limits*`, `mcp-needs-auth-cache.json` | Managed | Org/MCP state |

Full per-folder detail with naming patterns: [Directory reference](../domain/business-logic/directory-reference.md).

## Related Services

- [GitLab plugin](../domain/business-logic/plugins.md), Grafana Cloud, iTerm2 status script.

## Related Documentation

- [System overview](../architecture/system-overview.md)
- [Directory reference](../domain/business-logic/directory-reference.md)
