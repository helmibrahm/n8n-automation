# Custom API boundaries

[Documentation index](index.md) · [Workflow and integrations](workflow.md)

## 12. Custom API responsibilities

The historical workflow calls custom integrations over HTTP. FastAPI is the implementation technology identified by the operator; the exports show what n8n requests, not the helper code or its side effects. External service relationships below describe the business purpose at the call boundary.

| API responsibility | Visible call intent | Do not infer |
| --- | --- | --- |
| Messaging channel setup | Ask the Telegram integration to create a channel using prepared channel context. | User membership, messaging, bot administration, or successful creation. |
| Document-folder setup | Send deployment, channel and work-item context to a Nextcloud WebDAV-related helper. | A particular file copy, complete documentation pack, upload verification, or DNS update. Passing domain-related metadata is not a DNS mutation. |
| Server-related lookup and recording | Send server context to custom requests, including a Vultr-related lookup and follow-on record-oriented requests. | Provisioning a Vultr instance, configuring firewalls, obtaining shell access, or deploying an application. A create-like label on a custom API request is not proof of a cloud create action. |
| Variant-only helper | A separate server/document request is only trigger-reachable in one reviewed snapshot. | That this path ran, or that it is necessary for all deployments. |

Requests and results were reviewed at role level. No schemas copied from production, credential bindings, response samples, paths, hostnames, or API implementation are provided. Compare the [integration sequence](workflow.md#d07-integration-sequence) for the simplified caller view.

## Separate personal lab: co-location only

| Component | Verified placement | Known role |
| --- | --- | --- |
| Automation helper A | Homelab Docker, operator-confirmed | Custom automation helper |
| Automation helper B | Homelab Docker, operator-confirmed | Custom automation helper |
| Custom API backend | Homelab Docker, operator-confirmed | Separate FastAPI backend |

These components share a host with n8n. No relationship between this personal hosting setup and the historical employer workflow is established. No direct API call, container network, service authentication scheme, or shared storage was confirmed for these containers. The two helpers are not assumed to be part of the FastAPI backend. Their internal identifiers, routes and implementation details are intentionally omitted.

## Documenting a confirmed integration

Once the operator confirms a relationship that can be disclosed, record the caller and callee as aliases, direction, purpose, interface category, data sensitivity, authentication method category, timeout/retry behavior, and failure boundary. Link to a sanitized synthetic contract or example only if publication is authorized. Leave unknown fields empty or explicitly unknown; never infer an integration from co-location.

Use the [blank synthetic integration record](../examples/integration-record.example.yaml). Its example placeholders do not represent an actual call path.
