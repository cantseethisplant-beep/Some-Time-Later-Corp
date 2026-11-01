# MAP-031 — Build Sequence and Requirement Traceability (Assembly Stage 1 of 4)

**Task:** MAP-031 — Produce the build sequence and requirement traceability part of the candidate blueprint
**Claim worker:** hermes-laptop-map-031-auto-20261030
**Claim commit:** 98ece3b9aca490945632ceb2ebf3803c267bead4
**Output path:** docs/map/specs/loop-map-031-assembly.md
**Status:** unaccepted proposal for review only. Not accepted requirements, not technical evidence, no app implemented or tested.
**Assembly version:** 1 | **Assembly step:** 1 | **Loop policy:** 1 | **Loop kind:** assembly | **Loop cycle:** 5 | **Loop area:** build-and-acceptance | **Loop key:** candidate-assembly-v1-stage-1

## 1. Purpose, Scope, and Evidence Discipline

This document is Stage 1 of the four-stage candidate-blueprint package: (1) build sequence and requirement traceability, (2) component/data/interface map, (3) acceptance/evidence matrix with source pins and open decisions, (4) consolidated candidate blueprint and review handoff. Stages 1–3 use the same frozen immutable completed submissions and baseline; stage 4 also reads only completed, released assembly parts.

This stage bounds the proposed first implementation scope, lists explicit exclusions, defines stable step IDs B01 onward in prerequisite order, traces requirements to steps, and flags any requirement with no implementable step yet. It carries forward source evidence and unresolved policy labels without implying independent acceptance, completed tests, implementation, or deployment.

### 1.1 What this stage does

- Defines fixed assembly stages A–C with stable step IDs B01–B14 in prerequisite order. Acceptance-matrix assembly belongs to package Stage 3 and is not assembled here.
- For each step: purpose, inputs/source pins, component/artifact to build, outputs, dependencies, observable acceptance checks.
- Traces requirements REQ-01 through REQ-17 to steps and flags requirements with no implementable step yet.
- Includes controller/node/corporation boundaries, enrolment, permission checks, catalogue/deployment, operation reporting, scheduling, backup/restore, release/rollback, and isolation.
- States precise prerequisites where an owner choice or unverified upstream detail prevents exact instructions; never invents versions, commands, default policies, or completed checks.
- Proposes sequencing only; it is not an accepted architecture.

### 1.2 What this stage does not do

- No audits, generator tasks, technology-stack selection, cost estimates, test creation, or deployment.
- No rework of completed subjects merely to produce more prose.
- No external writes, GitHub operations, or branch creation.
- No acceptance-matrix assembly (that is package Stage 3).
- Unresolved policies remain unresolved; they never become mandates in examples.

### 1.3 Source inventory used

| Revision | Paths | Evidence type |
|---|---|---|
| 792b158838aa5214d0156690d24e21e780de542e | README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md | User-intent baseline; no upstream technical verification |
| c6cc2de20805455eb55c0343394d01225ff41ffd | docs/map/specs/requirements.md | Unaccepted draft for review only (MAP-001) |
| 3585afed129ad2694660fcee8cfd982092551117 | docs/map/specs/permissions.md | Unaccepted draft for review only (MAP-002) |
| 0e60848ccbfa295169422eab063f1b81023b390e | docs/map/specs/hosting-assignment.md | Unaccepted draft for review only (MAP-003) |
| ccf0957af0d80fe4608fc08b06b02408b485b1ca | docs/map/specs/backup-recovery.md | Unaccepted draft for review only (MAP-004) |
| 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 | docs/map/specs/catalogue-entry.md | Unaccepted draft for review only (MAP-005) |
| 111a5832102570811dd0af21fffd16a70413febc | docs/map/specs/operations.md | Unaccepted draft for review only (MAP-006) |
| 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 | docs/map/specs/scheduling.md | Unaccepted draft for review only (MAP-007) |
| 119bb89f6decab9c887e0e99bde38e7d6b1a6744 | docs/map/specs/evidence-record.md | Unaccepted draft for review only (MAP-011) |
| 39981db00918b363bc50f33cdb2dfe2dec22d210 | docs/map/specs/node-lifecycle.md | Unaccepted draft for review only (MAP-014) |
| 1cd788bd77c027a6808c3c4179784a77d8ca1efe | docs/map/specs/release-lifecycle.md | Unaccepted draft for review only (MAP-015) |
| 552d40b359af110eb85e67f58b774de80f2b5cf8 | docs/map/specs/loop-map-017-followup.md | Unaccepted draft for review only (MAP-017) |
| 41c48febc50f58304a164ebc4abe174e891193ee | docs/map/specs/loop-map-019-followup.md | Unaccepted draft for review only (MAP-019) |
| 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 | docs/map/specs/loop-map-023-followup.md | Unaccepted draft for review only (MAP-023) |
| 57dfe172304d5fcf2f19a98f3c16ccbd57131442 | docs/map/specs/loop-map-025-followup.md | Unaccepted draft for review only (MAP-025) |
| d45c7a945523ca05447cf8f9757b171fd319b5da | docs/map/specs/loop-map-026-followup.md | Unaccepted draft for review only (MAP-026) |
| 6b4aa91aebf4c07de0a9c239ad0b07eb0f6da2de | docs/map/specs/loop-map-027-followup.md | Unaccepted draft for review only (MAP-027) |
| 4e3dec35f8da85e6fb2668550fe592368a31fc22 | production/proposals/blueprint-005.json | Completed unaccepted audit for gap context only (MAP-030) |

### 1.4 Boundaries and blocks

Blocked prior assembly parts (coordination status only, not supplied documents): none.

This stage references but does not edit any source draft. Source drafts remain labelled with their actual evidence status. No stack, provider, cost, licence, retention value, or default policy is chosen here.

## 2. Build Sequence: Three Stages, Steps B01–B14

Assembly policy: fixed stages, no new audits or generator tasks. Steps use stable IDs B01 onward in prerequisite order. Package Stage 3 (acceptance matrix) is not assembled in this file.

### Stage A — Foundation and Boundaries

| Step | Purpose | Inputs/source pins | Component/artifact | Outputs | Dependencies | Observable acceptance checks |
|---|---|---|---|---|---|---|
| B01 | Establish controller boundary and roles matrix; separate deployment authority from backup decryption permission | docs/TRUST-AND-RECOVERY.md — Proposed roles; docs/DECISION-GUIDE.md — Questions still open; docs/map/specs/permissions.md | Role/action matrix record (proposed design) | Role matrix: five roles, seven actions; succession/emergency/delegation unresolved | None | Matrix lists five roles and seven actions; unresolved owner decisions marked unresolved |
| B02 | Establish catalogue entry states and evidence conditions (proposed schema only) | docs/map/specs/catalogue-entry.md — Sections 3, 4, 6 | Catalogue-entry schema record | Four entry states with required/optional field groups and invalidation triggers | None | Four states present; backup fields and restore fields separate; restore_verified never derived from backup upload |
| B03 | Establish hardware offer and assignment field inventories (proposed schema only) | docs/map/specs/hosting-assignment.md — Sections 3, 4, 5 | Offer and assignment field records | Offer fields and assignment fields; proposed assignability rule | None | Proposed assignment required subset explicit; missing backup_policy_ref makes offer draft/incomplete |
| B04 | Establish enrolment and withdrawal lifecycle states | docs/map/specs/node-lifecycle.md — Sections 2, 3, 4 | Node lifecycle state model | Eight states; revocation distinct from verified workload/data cleanup | B01 | Revocation separated from cleanup; identity/key mechanism unresolved |
| B05 | Establish operation status model and failure reporting | docs/map/specs/operations.md — Sections 3, 4, 5 | Operation state model | Nine states; timeout/unknown outcome handling; retry eligibility and idempotency rules | None | Success never inferred from launch; recovery-required distinct from failed |
| B06 | Establish time semantics for schedules, expiry, and movement windows | docs/map/specs/scheduling.md — Sections 3–7 | Time semantics record | UTC storage proposed (unresolved); explicit timezones; DST ambiguity; missed schedules; clock uncertainty | None | No default timezone or schedule invented; missed-schedule policy unresolved |

### Stage B — Deployment and Catalogue Placement

| Step | Purpose | Inputs/source pins | Component/artifact | Outputs | Dependencies | Observable acceptance checks |
|---|---|---|---|---|---|---|
| B07 | Define catalogue dependency-aware placement rules | docs/map/specs/catalogue-entry.md — Sections 4.2, 4.4; docs/CONCEPT.md — Dependency awareness | Dependency/placement rule record | Standalone vs add-on vs shared-service distinction; placement considers databases, jobs, persistent data | B02 | Entry type populated before placement; dependency_evidence unresolved where unconfirmed |
| B08 | Define controlled deployment preparation and verification step | docs/CONCEPT.md — Proposed journey step 5; docs/map/specs/release-lifecycle.md — Reviewed release stage | Deployment preparation record | Reviewed immutable version checked against host runtime; resource limits within owner offer | B02, B03 | Deployment verification passes on target host before assignment active (proposed, not verified) |
| B09 | Define release lifecycle stages and rollback limits | docs/map/specs/release-lifecycle.md — Release lifecycle stages, limits of rollback | Release lifecycle record | Proposed, reviewed, approved-for-environment, deployed, superseded, withdrawn; fencing rules; no two authoritative writers | B08 | Superseded release retained for rollback; rollback reason/procedure/outcome recorded if used |
| B10 | Define backup creation as distinct from restore verification | docs/map/specs/backup-recovery.md — Sections 2, 5, 6 | Backup/restore record concepts | Operation labels (Requested, Running, Verified copy, Failed); restore-tested categories; keys separate from encrypted copies | B05 | Upload success not recast as recoverability; failed restore does not overwrite verified-copy evidence |

### Stage C — Movement, Reporting, Recovery, and Rollout

| Step | Purpose | Inputs/source pins | Component/artifact | Outputs | Dependencies | Observable acceptance checks |
|---|---|---|---|---|---|---|
| B11 | Define planned move and fencing procedure | docs/TRUST-AND-RECOVERY.md — Backup and movement; docs/map/specs/operations.md — Section 6.3 | Movement procedure record | Destination consent and compatibility; quiesce; consistent state capture; verify destination; change routing; fence previous writer before new writes; stop-to-rollback on failure | B09 | Two authoritative writers never admitted merely because both hosts appear healthy |
| B12 | Define operation reporting and idempotency for moves/backups/deploys | docs/map/specs/operations.md — Sections 4, 5 | Operation reporting record | Idempotency keys; timeout and unknown outcome handling; error classes; retry rules unresolved | B05, B11 | Unknown outcome not auto-retried; launch alone never infers completion |
| B13 | Define recovery custodian access boundaries and emergency recovery outline | docs/TRUST-AND-RECOVERY.md — Proposed roles; docs/map/specs/permissions.md — Section 6 | Recovery access record | Custodian retrieves/restores authorised material only; deployment authority and decryption separate | B01, B04 | Decryption authority not assigned; custodian succession unresolved |
| B14 | Record repeatable rollout isolation principle (unsourced REQ-16 scope) | docs/map/specs/requirements.md — REQ-16 (unsourced); docs/DECISION-GUIDE.md — Build Idea 2 reusable product | Isolation principle record | Second isolated test corporation without copying first corporation's private data; isolation check proposed, not completed | B02 | REQ-16 marked unsourced/proposed-design-only; no baseline modality invented |

## 3. Requirement-to-Step Crosswalk

REQ-01 through REQ-17 come from docs/map/specs/requirements.md (MAP-001 draft, unaccepted review material). Status/modality labels are consolidation status only, not accepted requirements.

| REQ | Behaviour | Status | Modality | Implementable step(s) | Requirement flagged |
|---|---|---|---|---|---|
| REQ-01 | Corporation records administration and recovery contacts/custodians before assignments | required | intent | B01, B13 | No |
| REQ-02 | Members voluntarily offer hardware/VM/allocation with availability and permitted workloads | required | may | B03 | No |
| REQ-03 | CEO or appointed managers choose a reviewed bundle and inspect dependencies/resource requirements | required | intent | B07, B08 | No |
| REQ-04 | Assignment stays within owner consent and approved limits | required | should | B03, B08 | No — hard "must not exceed" gate is proposed-design |
| REQ-05 | Controlled deployment prepared and verified on an approved host before use | proposed | intent | B08 | No — verification proposed, not independently verified |
| REQ-06 | Authorised users monitor health; request backups or use scheduled backups | required | may | B05, B10 | No — health-status exposure has no explicit should |
| REQ-07 | Movement/recovery follows application-specific procedure recording success or attention items | required | intent | B11, B12 | No |
| REQ-08 | Assignment record fields: version, dependencies, host, limits, schedule, expiry, movement window, backup schedule, destination, retention, recovery custodians | proposed | could/may | B03 | No — retention and exact times undecided (OD-14) |
| REQ-09 | Manual and scheduled backups use one shared consistent procedure | proposed | should | B10 | No — identical procedure execution not evidenced |
| REQ-10 | Member hardware and optional corporation cloud resources recorded together; no cost/provider/retention targets preset | proposed | may | B02 | No — optional cloud recording; no spend limit assumed |
| REQ-11 | Catalogue marks each entry as standalone application, add-on, or shared service | proposed | must | B02 | No — entry type populated before placement is proposed design |
| REQ-12 | Placement considers databases, background jobs, persistent data, application-specific requirements | proposed | must | B07 | No — placement validation rule is proposed design |
| REQ-13 | Existing Discord communication functions not rebuilt or merely duplicated | proposed | should not | None yet | Yes — exclusion boundary only; no implementable step |
| REQ-14 | Entry "supported" only after upstream repo/licence, immutable reviewed version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update/rollback procedure, backup/restore evidence | proposed | must | B02 | No — supported state defined, upstream verification pending |
| REQ-15 | Scheduled/clicked backup yields consistent package protected in transit/at rest, integrity verified, completion/failure recorded; keys separate from encrypted copies | proposed | must | B10 | No — backup behaviour not technically verified |
| REQ-16 | Repeatable rollout to a second corporation without copying private data; isolation check proposed, not completed | proposed | none claimed — unsourced | None — B14 records isolation principle as proposed design only | Yes — unsourced row retained; no baseline citation |
| REQ-17 | Hardware owner may withdraw future hosting; withdrawal recorded; no new assignments on that host; no instant-deletion promise on offline machine | proposed | may | B04 | No — offline mechanics unresolved (OD-07) |

Requirements with no implementable step yet: REQ-13 (Discord non-duplication is an exclusion boundary, not a build step) and REQ-16 (unsourced rollout row; B14 records the isolation principle only as proposed design with no baseline source).

Open decisions carried forward (unresolved, not mandated): OD-01 through OD-14 as enumerated in docs/map/specs/loop-map-017-followup.md, including controller operator/pay, CEO identity/delegation/succession/emergency recovery, volunteer-host workload acceptability, OS/runtime/cloud provider, cloud spending-limit enforcement, recovery targets, offline withdrawal mechanics, data-reader consent, licensing model, decryption authority, automatic failover evidence, retention/exact assignment times.

## 4. Boundaries Included in This Scope

- Controller/node/corporation: controller boundary recorded in Stage A (no controller storage or hosting choice made); eight node lifecycle states in B04 (revocation ≠ verified cleanup); isolated test corporation principle under REQ-16 in B14 (no rollout evidence).
- Enrolment: offer → enrolment-pending → approved → active → disconnected → draining → revoked → retired; consent is the gate; identity/key mechanism unresolved (B04).
- Permission checks: five roles, seven actions; deployment authority and backup decryption separate; succession, emergency access, delegation unresolved (B01, B13).
- Catalogue/deployment: entry states, dependency-aware placement, controlled deployment preparation/verification, release lifecycle stages (B02, B07, B08, B09).
- Operation reporting: nine states; timeout/unknown outcome; retry/idempotency unresolved (B05, B12).
- Scheduling: time semantics; movement window vs migration promise; backup creation distinct from restore verification (B06).
- Backup/restore: operation labels; restore-tested categories; keys separate from encrypted copies; upload not proof of recoverability (B10).
- Release/rollback: six stages; fencing; rollback reason/procedure/outcome recorded; no two authoritative writers (B09, B11).
- Isolation: second isolated test corporation principle; no private-data copy; proposed, not completed (B14).

## 5. Exclusions and Unresolved Prerequisites

### Explicit exclusions

- No technology stack, operating system, deployment runtime, cloud provider, or licence selection.
- No cost figures, spend limits, or retention values.
- No component tests, integration tests, restore tests, or runtime verification.
- No Discord integration or duplication of existing Discord communication (REQ-13 boundary).
- No automatic failover (OD-13).
- No infrastructure provisioning, deployment execution, or external writes.

### Unresolved prerequisites (stated precisely, not invented)

1. Who operates and pays for the central controller (OD-01).
2. CEO identity, delegation, succession, and emergency recovery establishment (OD-02, OD-10).
3. Which workloads are acceptable on volunteer hosts vs trusted infrastructure (OD-03).
4. Operating systems, deployment runtime, and cloud provider for the pilot (OD-04).
5. Cloud spending-limit enforcement and over-capacity behaviour (OD-05).
6. Acceptable recovery time and data-loss targets per application (OD-06).
7. Hardware-owner withdrawal procedure while offline (OD-07).
8. Who may read each corporation data type and how consent is documented (OD-08).
9. Product licensing and distribution model (OD-09).
10. Decryption authority separate from deployment authority; who may decrypt (OD-11).
11. Automatic failover evidence required before assumption (OD-13).
12. Retention and exact assignment times (OD-14).
13. Upstream identity, version, licence for any catalogue candidate (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures, CorpTools) — none verified; GitHub listing alone proves nothing.

## 6. Limitations and Review Pending

- All checked drafts are unaccepted completed drafts for review only; this assembly is review input, not acceptance.
- Evidence type is user-intent baseline only; no upstream technical verification exists for any backup, restore, deployment, or hosting behaviour.
- No backup, restore, component, or integration test was performed, and none is claimed.
- Board state and file SHAs were not independently verified; no GitHub, terminal, network, or delegation tools are available.
- Modality was preserved; no unresolved policy was converted into a mandate in examples.
- Backup creation and restore verification remain distinct throughout; restore_verified is never derived from a backup record.
- This sequencing is proposed only; it is not an accepted architecture and not build-ready.

Review pending: yes. This draft is review input only. Acceptance rests with the project owner or an appointed reviewer; nothing is self-accepted. Up to two document corrections may apply under task policy; acceptance and any merge remain with the project owner or appointed reviewer.
