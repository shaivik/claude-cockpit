---
title: High-Level Diagram
summary: System context diagram showing Claude Code, ~/.claude and the external systems it talks to.
sources:
  - settings.json
  - plugins/known_marketplaces.json
  - mcp-needs-auth-cache.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# High-Level Diagram

## Diagram

```mermaid
flowchart LR
  User[Developer] --> CC[Claude Code CLI / VS Code]
  CC <--> Home[(~/.claude)]
  CC --> API[Anthropic API]
  CC --> MCP[MCP servers: GitLab, Figma, Sentry, ...]
  CC --> Hook[~/.config/iterm2/cc-status]
  CC -- OTLP metrics/logs --> Grafana[Grafana Cloud]
  Home -- plugin sync --> GH[GitHub claude-plugins-official]
  Org[Org admin] -- signed settings/policy --> Home
  CC -- uv run skill scripts --> Ext[Prometheus, Tempo, pganalyze, Postgres, outlet PCs]
```

## Components

| Component | Description |
|---|---|
| `~/.claude` | Config + state store ([overview](../overview/description.md)) |
| MCP servers | Several need auth (listed in `mcp-needs-auth-cache.json`) |
| Grafana Cloud | Target of OTLP export from managed settings |

## Communication Paths

| From → To | Protocol |
|---|---|
| Claude Code → Grafana | OTLP http/protobuf, 60 s interval |
| Claude Code → IDE | WebSocket (`ide/<n>.lock`) |
| Claude Code → hooks | local process exec |
| Marketplace → plugins | git/GitHub fetch |

## Related Documentation

- [System overview](system-overview.md)
- [Telemetry](../observability/telemetry.md)
