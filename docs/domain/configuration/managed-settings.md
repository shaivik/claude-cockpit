---
title: Managed Settings and Policy
summary: Org-pushed remote-settings and policy-limits files, their signatures, consent record and what they enforce.
sources:
  - remote-settings.json
  - remote-settings-consent.json
  - policy-limits.json
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Managed Settings and Policy

## Configuration sources

| File | Role |
|---|---|
| `remote-settings.json` | Org settings: enables Claude Code telemetry and OTLP metrics/logs export (http/protobuf, 60 s, Grafana Cloud ap-south-1). Contains an auth header — **secret, never copy**. |
| `remote-settings.json.signature.json`, `.signature-iat.json` | Signature and issued-at proving authenticity |
| `remote-settings.json.synced-at` | Last sync timestamp |
| `remote-settings-consent.json` | Consent record keyed by org UUID: `accountUuid`, `dangerousSettingsHash`, `updatedAt` |
| `policy-limits.json` (+ `.signature*`, `.stamp.json`) | Restrictions |

## Policy restrictions (current)

| Restriction | Allowed |
|---|---|
| `allow_remote_control` | false |
| `allow_quick_web_setup` | false |
| `enforce_web_search_mcp_isolation` | false |

Defaults: `remote_control_at_startup: false`. `compliance_taints`: empty.

## Behaviour

Synced at start-up; local edits are overwritten or invalidate the signature. If dangerous settings change, the hash changes and consent is requested again.

## Sensitive configuration handling

Treat `remote-settings.json` as a credential.

## Related Documentation

- [Telemetry](../../observability/telemetry.md)
- [Authorization](../../security/authorization.md)
