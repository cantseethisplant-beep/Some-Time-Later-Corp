# Build map

**Status: incomplete; no completed-map claim.** This index is integrated by the coordinator after task acceptance. Queue status and ownership live only in [the task board](../../production/board.json).

## Existing baseline

[Concept](../CONCEPT.md), [decision guide](../DECISION-GUIDE.md) and [trust/recovery intentions](../TRUST-AND-RECOVERY.md) record the agreed direction and unresolved options. They are requirements context, not verified upstream support.

## Initial independent work packages

| Task | Deliverable path | Purpose |
| --- | --- | --- |
| MAP-001 | specs/requirements.md | Stable requirements and glossary |
| MAP-002 | specs/permissions.md | Roles and action permissions |
| MAP-003 | specs/hosting-assignment.md | Hardware offer and assignment contract |
| MAP-004 | specs/backup-recovery.md | Backup and recovery behaviour |
| MAP-005 | specs/catalogue-entry.md | Catalogue and evidence contract |

These are planned paths, not completed documents. Each package is independent of the others and reads only the existing baseline. Conflicts discovered during integration become explicit follow-up work.

## Coverage still to complete

Requirements; glossary; roles and succession; catalogue; exact upstream identities, versions and licences; component compatibility; resource measurements; data model; public/private interfaces; node enrolment and isolation; secrets and key custody; controller hosting; cloud scope and spending; scheduling and timezones; backup/restore; movement and fencing; audit/status behaviour; updates and rollback; rollout instructions; costs; end-to-end build sequence and acceptance matrix.

Later tasks become ready only when their actual inputs are accepted. No technology stack or upstream support is implied by this list.

## Build-ready release

Apply docs/PRODUCTION.md's completion gate, resolve every build blocker, record all accepted evidence and freeze a map revision with a dated coverage review. The desired outcome is implementation from a checked map with targeted verification, without a fresh discovery phase. This repository has not reached that outcome yet.
