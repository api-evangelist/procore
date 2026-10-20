---
name: procore-submit-submittals
description: List and create submittals on a Procore project.
api: procore:procore-api
operations: [listProjects, listSubmittalsOnAProject, createSubmittal]
generated: '2026-10-20'
method: generated
---
1. `listProjects` with the `Procore-Company-Id` header to resolve the project.
2. `listSubmittalsOnAProject` to check for an existing submittal (no idempotency key on writes).
3. `createSubmittal` to create it. Back off on 429 using `X-Rate-Limit-Reset`.
