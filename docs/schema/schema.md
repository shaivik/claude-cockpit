---
title: File Formats and Naming Patterns
summary: Formats, naming regexes and key fields of every file family in ~/.claude (this directory has no database).
sources:
  - projects/
  - sessions/
  - file-history/
  - plugins/installed_plugins.json
  - backups/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Schema

## Database technology

Not applicable — state is stored as files. This page is the file-format equivalent of a schema.

## Schema overview

`<uuid>` = `[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}`. `<epoch-ms>` = 13-digit millisecond timestamp.

## Major entities

| Entity | Path pattern (regex-style) | Format | Key fields |
|---|---|---|---|
| Project folder | `projects/-[A-Za-z0-9_-]+/` | dir | cwd with `/` and `.` replaced by `-` (so `/Users/x/.claude` → `-Users-x--claude`) |
| Session transcript | `projects/<project>/<uuid>.jsonl` | JSONL | one message/tool event per line |
| Subagent transcript | `projects/<project>/<uuid>/subagents/agent-<hex>.{jsonl,meta.json}` | JSONL / JSON | subagent conversation and metadata |
| Tool result spill | `projects/<project>/<uuid>/tool-results/<id>.txt` | text | large tool output stored out of line |
| Memory | `projects/<project>/memory/{MEMORY.md,<topic>.md}` | markdown | index + one-fact notes with frontmatter |
| Prompt history | `history.jsonl` | JSONL | `display, pastedContents, timestamp, project, sessionId` |
| Live session | `sessions/<pid>.json` | JSON | `pid, sessionId, cwd, startedAt, version, kind, entrypoint, messagingSocketPath` |
| Session key | `sessions/<pid>.<sha256>.key` | opaque | per-session credential; do not share |
| Session env | `session-env/<uuid>/` | dir | per-session env (usually empty) |
| File snapshot | `file-history/<uuid>/<16-hex>@v<N>` | raw file copy | version N of a file edited in session |
| IDE lock | `ide/<port>.lock` | JSON | `pid, workspaceFolders, ideName, transport, authToken` |
| Config backup | `backups/.claude.json.backup.<epoch-ms>` | JSON | copy of `~/.claude.json` |
| Shell snapshot | `shell-snapshots/snapshot-<shell>-<epoch-ms>-<6-char>.sh` | shell | captured env/functions |
| Failed telemetry | `telemetry/1p_failed_events.<uuid>.<uuid>.json` | JSONL | `event_type, event_data` |
| Plugin install | `plugins/installed_plugins.json` | JSON v2 | `plugins.<name>@<marketplace>[] {scope, installPath, version, gitCommitSha}` |
| Plugin cache | `plugins/cache/<marketplace>/<plugin>/<12-hex>/` | dir | one folder per fetched version |
| Synced content | `{skills,plugins}/synced/<orgUuid>_<accountUuid>/` | dir | server-synced; `skills/synced/*/manifest.json` lists skills |
| Skill | `skills/<name>/SKILL.md` | md + frontmatter | `name`, `description` |

## Entity relationships

`history.jsonl.sessionId` = transcript filename = `file-history/<dir>` = `session-env/<dir>` = `sessions/<pid>.json.sessionId`. `history.jsonl.project` is the real cwd matching a `projects/` folder.

## Important relationships

Deleting a transcript removes resume ability but leaves `file-history/` and `history.jsonl` entries orphaned (harmless).

## Naming conventions

Kebab-case skill names; generated files use UUIDs or epoch-ms; dotfiles (`.last-cleanup`, `.last-update-result.json`) are housekeeping.

## Database constraints / Important indexes / Partitioning

Not applicable.

## Data ownership

Hand-edited: `CLAUDE.md`, `settings.json`, `skills/<custom>`, `plans/`. Claude Code owns the rest; Org admin owns `remote-settings*`, `policy-limits*`.

## Related Documentation

- [Directory reference](../domain/business-logic/directory-reference.md)
- [Sessions and memory](../domain/business-logic/sessions-and-memory.md)
