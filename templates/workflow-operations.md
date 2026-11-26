# Workflow operations template

Blank runbook. Document what an authorized operator should know; this file is not authorization to activate, deploy, or execute a workflow.

## Scope and readiness

- Workflow alias and owner role:
- Deployment status and evidence:
- Supported node versions and configuration categories:
- Required approvals and environment boundaries:
- Expected health signal and a sanitized test fixture:

## Failure and recovery

- Expected failure modes and operator-visible symptoms:
- Alert destination category and evidence of delivery:
- Retry and replay constraints; risk of duplicate side effects:
- Safe recovery order, restore prerequisites and last verified exercise:
- How to verify recovery without touching production data:

## Change and sharing checklist

- List exactly which configuration categories change, not their values.
- Record review evidence and actual test results before declaring readiness.
- Keep public examples inactive by default and confirm rights before sharing.
- Use the [safe export checklist](../docs/export-publication.md) before any export or publication.
