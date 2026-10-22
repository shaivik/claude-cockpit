---
title: Telemetry
summary: How Claude Code usage telemetry is exported via OTLP and queued locally, plus logs and debug files.
sources:
  - remote-settings.json
  - settings.json
  - telemetry/
  - debug/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Telemetry

## Logging

`debug/latest` → symlink to the most recent debug log (the target may not exist). Session history is in `projects/`.

## Metrics / Tracing / Telemetry architecture

Managed settings enable Claude Code telemetry and export OpenTelemetry **metrics and logs** over http/protobuf every 60 s to a Grafana Cloud OTLP gateway (ap-south-1). Traces: unknown from source. Resource attributes come from `settings.json` (`developer.email`, `team.id=ops-tech`).

## Local queue

`telemetry/1p_failed_events.<session-uuid>.<uuid>.json` holds first-party events that failed to send (e.g. `tengu_feature_sad`, 2026-10-06). Safe to delete.

## Important metrics / log fields / Trace propagation / Dashboards / SLO

Unknown from source — see [FAQs](../references/faqs.md#open-questions).

## Health checks / Dependency monitoring

Not applicable.

## Related Documentation

- [Managed settings](../domain/configuration/managed-settings.md)
- [Alerting](alerting.md)
