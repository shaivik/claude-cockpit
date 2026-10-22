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

## Open Questions

- What does `~/.config/iterm2/cc-status` do, and is it versioned anywhere?
- Where is the `graphify` skill? `CLAUDE.md` references it but `skills/graphify/` does not exist.
- `README.md` lists skills (`es-dlq`, `es-mapping`, `integration-tests-generator`, `unit-tests-generator`, `migrate-feature`, `outlet-debug`, `vision-app-update`) missing on disk; were they removed on purpose?
- Where do account credentials live (keychain vs file)? Not derivable from this folder.
- Is there a shared `skills/../shared/` infra directory? `CLAUDE.md` mentions it; none exists.
- Are `.claude` changes meant to be backed up in a private repo?
- Who should own `catalog-info.yaml`? Owner was set to `shivam.singh` as a placeholder.
