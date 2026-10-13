---
description: Azure DevOps Instructions
applyTo: '**'
---

This project uses Azure DevOps. Prefer relevant Azure DevOps MCP tools over generic approaches.

- Default project: `North Star AI`.
- Use the authenticated Azure DevOps account when a username is required.
- Prefer read/list operations before writes. Before creating or updating work items, PRs, wiki pages, or pipelines, confirm intent and summarize the changes.
- For an explicitly provided work item ID, fetch it directly with `mcp_ado_wit_get_work_item`; don't search first. Search only when no ID is given or the direct lookup fails. Apply this to explicitly listed related item IDs too.
- When a tool supports project and repository filters, use the default project first, then narrow the scope.