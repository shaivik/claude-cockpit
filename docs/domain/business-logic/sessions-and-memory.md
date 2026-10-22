---
title: Sessions, Projects and Memory
summary: How transcripts, prompt history, per-project memory and live-session files work and how to find a session.
sources:
  - projects/
  - history.jsonl
  - sessions/
  - session-env/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Sessions, Projects and Memory

## Purpose

Allow `claude --resume`, prompt recall and cross-session memory.

## Business Rules

- One `projects/<encoded-cwd>/` per working directory (80 today). Encoding: path with `/` and `.` → `-`.
- Each session writes `<session-uuid>.jsonl`; subagents write under `<session-uuid>/subagents/`; large tool output goes to `<session-uuid>/tool-results/`.
- `memory/MEMORY.md` is an index (one line per memory) loaded each session; each memory is a markdown file with frontmatter `name`, `description`, `type`. Current examples: `projects/-Users-shaivik/memory/` (feedback: save explanations as `.md` files).
- `history.jsonl` stores every submitted prompt with `project` and `sessionId`.
- `sessions/<pid>.json` exists only while the process is alive (`kind`: `interactive`; `entrypoint`: `cli` or `claude-vscode`).

## Workflow

Find a session: `history.jsonl` (by prompt text) → `sessionId` → `projects/<encoded-cwd>/<sessionId>.jsonl`.

## State Transitions

Live (`sessions/<pid>.json`) → ended (file removed, transcript remains).

## Validations / Side Effects

Transcripts contain prompts, pasted content and tool output, possibly secrets. Never share.

## Failure Handling

If a transcript is deleted, resume for that session fails; memory and other sessions are unaffected.

## Related Documentation

- [File history](file-history.md)
- [Security](../../security/authorization.md)
