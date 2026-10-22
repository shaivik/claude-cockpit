---
title: System Overview
summary: How Claude Code reads config from ~/.claude and writes runtime state back, and where each concern lives.
sources:
  - README.md
  - settings.json
  - sessions/
  - projects/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# System Overview

## Architecture Summary

Claude Code (CLI or IDE extension) is the only process. At start it **reads** config (`CLAUDE.md`, `settings.json`, skills, plugins, managed settings) and during a session it **writes** transcripts, snapshots, caches and telemetry. There is no server component.

## Major Components

| Component | Paths | Role |
|---|---|---|
| Config | `CLAUDE.md`, `settings.json` | User-controlled behaviour |
| Managed config | `remote-settings*.json`, `policy-limits*.json` | Org-pushed, signed |
| Extensions | `skills/`, `plugins/` | Workflows and plugins |
| Session state | `projects/`, `sessions/`, `session-env/`, `history.jsonl` | Resume and history |
| Safety net | `file-history/`, `backups/` | Rewind and config backups |
| Caches | `cache/`, `shell-snapshots/`, `state/`, `mcp-needs-auth-cache.json` | Performance |
| Telemetry | `telemetry/`, OTLP export | Usage reporting |

## Component Responsibilities

See [directory reference](../domain/business-logic/directory-reference.md).

## Component Interactions

- Hooks in `settings.json` run `cc-status` on each lifecycle event.
- Skills run scripts with `uv run` and call external systems.
- Plugins add skills/MCP servers whose auth state is cached in `mcp-needs-auth-cache.json`.

## Request Flow

1. User prompt → appended to `history.jsonl`.
2. Claude Code loads `CLAUDE.md`, settings, skill descriptions and memory.
3. Tool calls pass permission rules, then hooks fire (Pre/PostToolUse).
4. Transcript line appended to `projects/<encoded-cwd>/<session>.jsonl`; edited files snapshotted to `file-history/<session>/`.

## Event Flow

Not applicable — no message broker. Lifecycle events are only hook triggers ([hooks](../domain/business-logic/hooks.md)).

## External Dependencies

Anthropic API, GitHub marketplace, Grafana Cloud OTLP, MCP servers.

## Failure Boundaries

- Hook failure does not corrupt state (timeouts of 5 s on most hooks).
- Corrupt or deleted `projects/` entries only lose resumability.
- Edits to managed files are overwritten at next sync.

## Architectural Decisions

None recorded. See [FAQs](../references/faqs.md#open-questions).

## Trade-offs

- Everything is plain files: simple to inspect, but transcripts accumulate (`projects/` is ~226 MB) and contain sensitive data.

## Related Documentation

- [High-level diagram](high-level-diagram.md)
- [Low-level diagram](low-level-diagram.md)
- [Security](../security/authentication.md)
