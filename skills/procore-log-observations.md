---
name: procore-log-observations
description: Record field observations in Procore and restore a deleted incident from the recycle bin.
api: procore:procore-api
operations: [listObservationItems, createObservationItem, retrieveRecycledIncident]
generated: '2026-10-20'
method: generated
---
1. `listObservationItems` to see what is already logged.
2. `createObservationItem` to log a new observation.
3. A deleted incident can be taken back with `retrieveRecycledIncident` (recycle-bin restore; no window is stated in the contract).
