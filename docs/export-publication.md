# Safe workflow export and publication

No real workflows or exports are included. Prefer a narrative and sanitized diagram over exporting a live workflow. Publication requires confirmation that the workflow and any embedded scripts are authorized to share, plus approval for the exact outgoing files and remote action.

## Prepare an authorized example offline

1. Start from an approved definition or a synthetic example. Keep the original out of the repository. Never export credentials, execution history or binary production data. Keep any import inactive by default.
2. Review the entire copy recursively. Remove credential bindings, credential names and IDs, auth headers and query tokens, private hosts, URLs and webhook details, identifiers, environment references that reveal private configuration, and any node parameters imported from a command that carried authentication.
3. Remove pinned data, execution samples, cached payloads, production binary references, sensitive node notes and proprietary expressions or code. Supply synthetic fixtures only where needed and approved.
4. Check node versions, required capabilities by category, data shape, and import guidance. If authorized, validate importability in an isolated instance with mocks and no outbound production access. Record what was actually tested. Do not activate or execute anything against live systems.
5. Re-scan the exact staged files and outgoing commits, including docs, screenshots, attachments, examples and history. Report findings by file and category, never by secret value. If a secret was already published, stop and request an incident response rather than rewriting remote history.

## Publish only after review

Review the intended audience, rights, and the public detail level of the document. Verify that example links are local and that private logs, data, and live settings are ignored and untracked. Commit only a reviewed staged diff. Push and remote repository changes always require separate explicit approval.
