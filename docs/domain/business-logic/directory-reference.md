---
title: Directory Reference
summary: Per-folder and per-file usage guide for every entry in ~/.claude, with who writes it and whether it is safe to delete.
sources:
  - README.md
  - settings.json
  - skills/
  - plugins/
  - projects/
  - file-history/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Directory Reference

Every top-level entry, its writer and its cleanup safety. Sizes as of 2026-10-22. Naming patterns are in [schema](../../schema/schema.md).

## Purpose

Answer "what is this folder for and can I delete it?".

## Business Rules

Legend — **Edit**: you maintain it · **Gen**: Claude Code writes it · **Mgd**: org/server managed, do not edit.

### Config and instructions

| Path | Kind | Usage | Delete? |
|---|---|---|---|
| `CLAUDE.md` | Edit | Global instructions loaded in every project ([page](../configuration/claude-md.md)) | No |
| `settings.json` | Edit | Env, permissions, hooks, model, plugins, UI ([page](../configuration/settings.md)) | No |
| `remote-settings.json` (+ `.signature*.json`, `.synced-at`) | Mgd | Org telemetry settings; contains an auth header ([page](../configuration/managed-settings.md)) | No |
| `remote-settings-consent.json` | Gen | Records consent to dangerous managed settings (hash + timestamp) | Re-prompts |
| `policy-limits.json` (+ `.signature*`, `.stamp.json`) | Mgd | Org restrictions (remote control, quick web setup, web search isolation) | No |
| `mcp-needs-auth-cache.json` | Gen | MCP servers awaiting auth, with timestamps | Yes |

### Extensions

| Path | Kind | Usage | Delete? |
|---|---|---|---|
| `skills/<name>/` | Edit | Custom skills ([page](skills-system.md)) | No |
| `skills/synced/<org>_<acct>/` | Mgd | Account-synced skills (`docs`, `docx`, `pdf`, `pptx`, `xlsx`, `morning`, `skill-creator`, …) + `manifest.json` | Re-syncs |
| `plugins/installed_plugins.json` | Gen | Installed plugin list | No |
| `plugins/known_marketplaces.json` | Gen | Registered marketplaces | No |
| `plugins/marketplaces/<name>/` | Gen | Cloned marketplace repo | Re-clones |
| `plugins/cache/<marketplace>/<plugin>/<sha>/` | Gen | One folder per downloaded plugin version; older SHAs are stale | Yes (old SHAs) |
| `plugins/store/`, `plugins/synced/`, `plugins/.trash/` | Gen | Diff store, synced plugins, trashed installs | Yes (`.trash`) |
| `plugins/*-cache*.json` | Gen | Install-count and directory caches | Yes |

### Session state

| Path | Kind | Usage | Delete? |
|---|---|---|---|
| `projects/<encoded-cwd>/` | Gen | Transcripts, subagent logs, tool-result spills, `memory/` ([page](sessions-and-memory.md)) | Loses resume/memory |
| `history.jsonl` | Gen | Prompt history for up-arrow recall | Loses history |
| `sessions/` | Gen | One `<pid>.json` + `.key` per live process | Stale ones only |
| `session-env/<uuid>/` | Gen | Per-session env dir (80+ entries, mostly empty) | Yes |
| `file-history/<uuid>/` | Gen | File snapshots for rewind ([page](file-history.md)) | Old ones |
| `shell-snapshots/` | Gen | Captured zsh environment reused by Bash tool | Yes |
| `plans/` | Edit/Gen | Saved plan-mode documents | Keep |

### Caches and housekeeping

| Path | Kind | Usage | Delete? |
|---|---|---|---|
| `cache/changelog.md`, `cache/model-catalog/` | Gen | Changelog and model catalog | Yes |
| `telemetry/` | Gen | Failed first-party telemetry events queued for retry | Yes |
| `debug/latest` | Gen | Symlink to latest debug log | Yes |
| `downloads/` | Gen | Downloaded attachments (empty) | Yes |
| `backups/` | Gen | Rolling backups of `~/.claude.json` | Old ones |
| `ide/<port>.lock` | Gen | IDE connection lock (workspace folders + token) | Stale ones |
| `state/mcp-discover-verdicts.json` | Gen | MCP discovery protocol verdicts | Yes |
| `.last-cleanup`, `.last-update-result.json` | Gen | Cleanup timestamp; last auto-update outcome | Yes |
| `docs/` | Edit | This documentation | — |

## Workflow

Edit-me files change by hand; everything else changes as a side effect of running `claude`.

## State Transitions

Not applicable.

## Validations

Never edit `*.signature*.json` or `remote-settings*`; signatures will fail and the file is re-synced.

## Side Effects

`projects/` holds full prompts and tool output; treat as sensitive.

## Failure Handling

Missing generated files are recreated on next run.

## Related Documentation

- [Backup and restore](../../operations/backup-restore.md)
- [Scaling and cleanup](../../operations/scaling.md)
