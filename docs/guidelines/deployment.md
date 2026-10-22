---
title: Deployment Guidelines
summary: Procedure for applying and validating changes to skills and settings, as there is no deployment pipeline.
sources:
  - settings.json
  - skills/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Deployment Guidelines

## Deployment prerequisites / procedure

1. Edit the file (`settings.json`, `skills/<name>/…`).
2. Validate JSON (`python3 -m json.tool settings.json`).
3. Start a new session or run the skill.

## Pre-deployment checklist

Hook script exists; no secrets in files you may copy; skill `description` has a trigger phrase.

## Post-deployment validation / Rollback

Run `/skills` or `/hooks`, invoke the skill once. Roll back from your own backup ([backup](../operations/backup-restore.md)).

## Environment promotion / Database migration

Not applicable.

## Production troubleshooting

See [setup troubleshooting](../overview/setup-instructions.md#troubleshooting).

## Related Documentation

- [CD](../ci-cd/cd.md)
