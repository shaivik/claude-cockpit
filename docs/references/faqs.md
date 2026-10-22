---
title: FAQs
summary: Frequently asked questions about ~/.claude and the open questions that could not be derived from files.
sources:
  - README.md
  - CLAUDE.md
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# FAQs

| Question | Answer |
|---|---|
| Can I delete `projects/`? | Yes, but you lose resume and memory ([directory reference](../domain/business-logic/directory-reference.md)). |
| Why are my edits to `remote-settings.json` gone? | It is managed and re-synced. |
| How do I find a past session? | Search `history.jsonl`, then open `projects/<encoded-cwd>/<sessionId>.jsonl`. |
| Where do `$SKILL_DIR` scripts live? | `~/.claude/skills/<name>/scripts/`. |
