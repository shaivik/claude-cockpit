---
title: CI
summary: States that ~/.claude has no CI pipeline and notes the CI-related permission rules and skill tests.
sources:
  - settings.json
  - skills/security-audit/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# CI

Not applicable — the directory is not under version control and has no pipeline (no `.gitlab-ci.yml`, no `.git`).

| Topic | Note |
|---|---|
| Related access | `glab ci list/view/trace` are allowed, `glab ci delete` is denied ([settings](../domain/configuration/settings.md)) |
| Tests | Only `skills/security-audit/validate-*.test.cjs` ([testing](../guidelines/testing.md)) |

## Related Documentation

- [CD](cd.md)
