---
title: Skills Catalogue
summary: Per-skill table of every custom and synced skill, its trigger, entry script and external systems.
sources:
  - skills/
  - skills/synced/
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Skills Catalogue

## Purpose

Lookup of what each skill does and where its code lives. Generic mechanics: [skills system](../../business-logic/skills-system.md).

## Custom skills (`skills/<name>/`)

| Skill | Trigger / use | Entry point | Extra files | External systems |
|---|---|---|---|---|
| `data-scientist` | Train/evaluate CV model for photo audits (SAM 3 labelling, YOLOv8n, 100% precision sweep) | `scripts/cv_audit.py` | `_data.py`, `_labeler.py`, `_trainer.py`, `_evaluator.py`, `notes.md` | AuditDB.csv, models |
| `db-schema` | Fetch and review PostgreSQL schema | `scripts/fetch_schema.py` | `_schema.py` | Postgres |
| `docs-generator` | Generate/sync `docs/` (this folder was produced with it) | `scripts/docs_generator.py` | `_backup.py`, `_lint.py`, `_mkdocs.py`, `references/` | filesystem, git |
| `endpoint-audit` | Audit a Rails endpoint or Sidekiq worker | `scripts/audit_endpoint.py` | `_prometheus.py`, `_tempo.py`, `_pganalyze.py` | Prometheus, Tempo, pganalyze |
| `prom-metrics` | CPU/memory profile of a k8s deployment | `scripts/fetch_metrics.py` | `queries.yaml`, `application_infra_configs/*.yml` (one per service) | Prometheus |
| `security-audit` | Security reviews and pen tests | none (markdown playbooks) | topic guides (`WEB-PROTOCOL-AND-AUTH.md`, …), `validate-*.cjs`, `report-schema.json` | none |
| `swiftui-migrator` | UIKit → SwiftUI (audit / plan / migrate) | none | `instructions.md` | EatClub iOS repo |

## Synced skills (`skills/synced/<org>_<acct>/<name>/`)

`docs`, `docx`, `pdf`, `pptx`, `xlsx`, `morning`, `import-memory`, `google-workspace`, `skill-analysis`, `skill-creator`, `eatclub-postgres-query`. Managed by the account; list in `manifest.json`.

## Notes

- Skills listed in `README.md` but absent on disk: `es-dlq`, `es-mapping`, `integration-tests-generator`, `unit-tests-generator`, `migrate-feature`, `outlet-debug`, `vision-app-update`, `graphify`.
- Invocation: `/<name> [args]`.

## Related Documentation

- [Skills system](../../business-logic/skills-system.md)
- [Workers overview](../overview.md)
