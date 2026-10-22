---
title: Alerting
summary: Confirms no alerts are defined and lists the local notification mechanisms.
sources:
  - settings.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Alerting

## Alert catalogue

None defined in this directory. Org-side alerts on the Grafana data, if any, are unknown from source.

## Local notifications

The `Notification`, `Stop` and `StopFailure` hooks call `cc-status` ([hooks](../domain/business-logic/hooks.md)) to signal state in iTerm2.

## Severity / Owner / Runbook / Escalation

Not applicable.

## Related Documentation

- [Telemetry](telemetry.md)
