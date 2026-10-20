---
name: procore-manage-rfis
description: Find a Procore project and list, create, update and reply to RFIs on it.
api: procore:procore-api
operations: [listCompanies, listProjects, listRfis, showRfi, createRfi, updateRfi, createRfiReply]
generated: '2026-10-20'
method: generated
---
1. `listCompanies` to get the company id; send it as the `Procore-Company-Id` header on every later call.
2. `listProjects` to resolve the project id (paginate with `page`/`per_page`).
3. `listRfis` (filters[...] supported) or `showRfi` to read existing RFIs.
4. `createRfi` / `updateRfi` to write; `createRfiReply` to answer.
Writes carry no idempotency key: check with `listRfis` before retrying a create. On 429 wait until `X-Rate-Limit-Reset`.
