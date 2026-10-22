---
title: Hooks
summary: Which lifecycle events run hooks in settings.json and what the iTerm2 cc-status command does.
sources:
  - settings.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Hooks

## Purpose

Drive an iTerm2 status indicator from Claude Code lifecycle events.

## Business Rules

| Event | Command | Timeout |
|---|---|---|
| SessionStart, SessionEnd, UserPromptSubmit, PermissionRequest, Notification, Stop, StopFailure | `/Users/shaivik/.config/iterm2/cc-status` | 5 s |
| PreToolUse, PostToolUse, SubagentStop | same | default |

All hooks are `type: command` with no matcher, so they fire for every tool. The script is outside this repo; its behaviour is unknown from source.

## Failure Handling

A missing script produces hook errors on each event but does not block work.

## Related Documentation

- [Settings](../configuration/settings.md)
- [FAQs](../../references/faqs.md#open-questions)
