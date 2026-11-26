# Workflow design template

Blank template only. Do not treat any field as a deployed workflow or publish a filled version without review.

| Field | Document the confirmed value |
| --- | --- |
| Workflow name | Public-safe alias |
| Purpose | User outcome and scope |
| Evidence and status | Verified, operator-confirmed, proposed, or unknown |
| Trigger | Category and scheduling intent, not a private webhook or URL |
| Inputs and outputs | Schema summary and synthetic examples only |
| Steps | Ordered role-level actions; identify unknown steps |
| Dependencies | Confirmed service aliases and the reason each is needed |
| Data handling | Sensitivity category, retention and redaction expectations |
| Credentials | Required permission categories only; no bindings, IDs or values |
| Failure behavior | Timeout, retries, idempotency boundary and responsible role |
| Verification | Fixture used, actual result, and any unverified paths |

## Diagram notes

Add Mermaid only after the trigger, transformations, destinations and edges are confirmed and approved for disclosure. Keep the text description complete without the diagram. Do not use real addresses, service paths, identities or example payloads taken from execution history.
