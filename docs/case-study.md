# Engineering case study and results

[Documentation index](index.md) · [Before and after](process.md) · [Workflow and integrations](workflow.md)

## 13. Error handling and operational limitations

| Failure boundary | Existing behavior or risk |
| --- | --- |
| Ineligible inputs | Row filtering and field normalization decide what enters the batch. The review does not establish a separate rejection report or comprehensive validation. |
| Existing work items | Conditional branches reuse references or issue create requests. This is not a system-wide idempotency guarantee; a lookup and a create are separate actions. |
| Integration timeout or failed action | The reviewed snapshots do not establish a dedicated error workflow, adaptive retries, compensation, or alerts. A runtime fault may interrupt downstream processing. |
| Partial success | Work-item writes, channel creation, folder operations, and register updates are separate side effects. A failure after an external write can leave the record incomplete; a blind rerun can repeat an action. |
| Variant and live state | One helper request is disconnected in one snapshot and connected in the other. Neither the snapshot with more wiring nor the supporting notes establish what ran in production. |
| Human review | A completed workflow or updated row is not evidence that a server works, an app is reachable, or a tender deliverable was approved. |

## 14. Measured business impact

| Historical deployment throughput | User-confirmed measured range |
| --- | --- |
| Before automation | Approximately 5–10 deployments per day |
| After introducing automation | Approximately 20–30 deployments per day |

These figures describe my broader deployment operation before and after introducing automation. They do not isolate how much of the change came from this specific n8n workflow or from any individual integration. I have not supplied a measurement period, per-deployment time savings, financial savings, or other quantitative outcomes.

## 15. Engineering decisions and personal contributions

I was the primary DevOps engineer responsible for 47 production servers. My role covered cloud provisioning, application configuration, domain setup, messaging channels, and deployment documentation. I used n8n and custom FastAPI integrations to reduce repeated coordination work without making the workflow responsible for every infrastructure change.

| Decision | Why I used it | Trade-off |
| --- | --- | --- |
| Start with the existing deployment register | Operators could work from the same deployment inputs instead of re-entering them into each tool. | Sheet structure and row matching become part of the contract. Concurrent edits and replay deserve separate tests. |
| Look up work items before creating them | Preserve task continuity where a match exists, and keep relations in the work tracker. | Lookup and create are distinct requests, so duplicate or racing runs are still possible. |
| Keep service-specific work behind custom APIs | n8n can coordinate channel, folder and server-related operations without describing every service's internal details in the workflow. | Helper failures can create partial results; request and response boundaries need explicit tests. |
| Keep the reviewed workflow manually initiated | Leave the start of deployment-support processing under operator control. | A run can be missed or repeated. GitLab deployment notes do not provide evidence of an event-driven n8n entry. |

## 16. Verification and historical usage

| Evidence | What it establishes | What it does not establish |
| --- | --- | --- |
| Firsthand historical account | I used automation in deployment operations and measured the change in throughput shown above. | Run history, per-branch success, or causality attributable only to n8n. |
| Two saved workflow snapshots, reviewed offline | Manual trigger, node reachability, work-item logic, helper intent at the HTTP boundary, selected writeback, and a connection difference. | Current activation, working credentials, external response behavior, or what exact revision was in use. |
| Supporting deployment notes, reviewed offline | A separate GitLab CI context and Nextcloud document handling practices. | A GitLab-to-n8n trigger or a successful end-to-end tender documentation run. |
| Portfolio review | Offline rendering, link/fragment validation and a sensitive-information review of intended files. | Runtime validation of the workflow, APIs, or integrations. |

No original workflow was imported or executed, and no live integration was contacted. Private source evidence stays outside the portfolio. The checks in the [requirements matrix](requirements.md#6-functional-requirements) are suggested, not executed.

## 17. Future improvements

1. **Make replays safer.** Use a stable deployment correlation key and track success for each external effect. Test timeout-after-write and duplicate input before allowing automated retries.
2. **Add visible partial outcomes.** In an isolated demo, record completed, failed and skipped actions separately; keep the result recoverable when the sheet writeback fails.
3. **Build a synthetic integration test harness.** Mock a sheet read/update, work-item lookup/create/relate, and both helper success and failure. Use fictional data only.
4. **Review trigger automation as a separate decision.** If an event-driven entry is wanted, verify permissions, event provenance, replay protection and human review expectations before adding it. Nothing here implements that path.
5. **Define operational and publication boundaries.** Document what belongs in a deployment handover and which artifacts can be shared. Use the [release checklist](export-publication.md) for any future authorized example.
