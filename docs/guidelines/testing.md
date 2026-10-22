---
title: Testing
summary: Test coverage available for skills in ~/.claude and how to run it.
sources:
  - skills/security-audit/validate-findings.test.cjs
  - skills/security-audit/validate-coverage-ledger.test.cjs
status: generated
last_reviewed: 2026-10-22
owner: shivam.singh
---

# Testing

## Testing strategy

Skills are validated by use. Only `security-audit` ships automated tests.

## Unit tests

| Test | Covers |
|---|---|
| `skills/security-audit/validate-findings.test.cjs` | `validate-findings.cjs` against `report-schema.json` |
| `skills/security-audit/validate-coverage-ledger.test.cjs` | `validate-coverage-ledger.cjs` |

Run locally: `node --test skills/security-audit/*.test.cjs` (assumes Node's built-in runner; verify).

## Others

Integration, system, API, contract, performance tests, coverage expectations and CI execution: not applicable. `docs-generator` `finalize` acts as a docs quality gate.

## Related Documentation

- [CI](../ci-cd/ci.md)
