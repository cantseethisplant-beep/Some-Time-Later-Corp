# Build map

**Status: incomplete; no completed-map claim.** This index is integrated by the coordinator after task acceptance. Queue status and ownership live only in [the task board](../../production/board.json).

## Existing baseline

[Concept](../CONCEPT.md), [decision guide](../DECISION-GUIDE.md) and [trust/recovery intentions](../TRUST-AND-RECOVERY.md) record the agreed direction and unresolved options. They are requirements context, not verified upstream support.

## Independent work packages

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

## Expanded work packages

| Task | Planned deliverable | Purpose |
| --- | --- | --- |
| MAP-006 | specs/operations.md | Define operation status and failure reporting |
| MAP-007 | specs/scheduling.md | Define scheduling and time semantics |
| MAP-008 | specs/controller-outage.md | Define controller outage behaviour |
| MAP-009 | specs/information-boundary.md | Define public/private information handling |
| MAP-010 | specs/pilot-brief.md | Prepare the pilot decision brief |
| MAP-011 | specs/evidence-record.md | Define map-wide evidence and invalidation records |
| MAP-012 | production/proposals/batch-001.json and .md (repository root) | Propose the next independent task batch |
| MAP-013 | specs/cloud-cost-controls.md | Define cloud scope and spending guardrails |
| MAP-014 | specs/node-lifecycle.md | Define node enrolment and withdrawal lifecycle |
| MAP-015 | specs/release-lifecycle.md | Define application release and rollback lifecycle |

All listed deliverables are planned, not complete. The live board holds ownership and acceptance state. MAP-012 follows the bounded task-generation recipe, proposes work only, and can be replaced by a new generator task after acceptance when useful gaps remain.
