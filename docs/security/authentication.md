---
title: Authentication
summary: How Claude Code authenticates the account, IDE connections, sessions and MCP servers, and where credentials sit on disk.
sources:
  - ide/
  - sessions/
  - mcp-needs-auth-cache.json
  - remote-settings.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Authentication

## Authentication mechanism

Account login to Anthropic (credentials held outside this folder, e.g. OS keychain — unverified).

## Identity provider

Anthropic account/org; org UUID visible in `synced/` folder names.

## Token/session mechanism

| Artifact | Credential |
|---|---|
| `ide/<port>.lock` | `authToken` for the IDE WebSocket (mode 600) |
| `sessions/<pid>.<sha256>.key` | per-session key (mode 600) |
| `remote-settings.json` | OTLP auth header |
| `*.signature.json` | integrity signatures, not credentials |

## Token lifecycle

Lock and session files are created at start and removed on exit; stale ones may remain.

## Login flow / Credential rotation

Unknown from source — see [FAQs](../references/faqs.md#open-questions).

## Service-to-service / API authentication

MCP servers listed in `mcp-needs-auth-cache.json` (GitLab, Figma, Swiggy Instamart, Atlassian, Amplitude, Hex) require OAuth via `/mcp`.

## Authentication failure behavior

Unauthenticated MCP servers are skipped and their tools are unavailable.

## Related Documentation

- [Authorization](authorization.md)
- [Managed settings](../domain/configuration/managed-settings.md)
