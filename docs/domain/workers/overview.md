---
title: Workers (Skills) Overview
summary: There are no background workers; skills are the closest analogue and run on demand.
sources:
  - skills/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Workers Overview

No background workers or schedulers live here. Skills run on demand inside a session; per-skill detail is in the [skills catalogue](files/skills-catalogue.md).

## Dependencies

`uv`, Python, network access to each skill's target systems.

## Failure Behavior

A failing script returns an error to the session; nothing retries automatically.

## Related Documentation

- [Skills system](../business-logic/skills-system.md)
