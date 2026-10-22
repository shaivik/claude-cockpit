---
title: File History and Rewind
summary: How file snapshots in file-history/ enable rewinding edits made by Claude, and how to prune them.
sources:
  - file-history/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# File History and Rewind

## Purpose

Before Claude edits a file, a copy is stored so the session can be rewound.

## Business Rules

- Path: `file-history/<session-uuid>/<16-hex>@v<N>`. The hash identifies the original file path; `N` increments per snapshot.
- ~49 session folders, ~870 snapshot files, ~3.9 MB.
- Snapshots are raw file contents — they can contain secrets from edited files.

## Workflow

Rewind (`/rewind` or Esc Esc) restores the snapshot for the chosen point.

## Failure Handling

Pruned snapshots only disable rewind for that session.

## Related Documentation

- [Sessions and memory](sessions-and-memory.md)
- [Scaling and cleanup](../../operations/scaling.md)
