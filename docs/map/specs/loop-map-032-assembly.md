# MAP-032 Assembly — Component, Data and Interface Map

**Task:** MAP-032 — Component, data and interface map (architectural map of the candidate blueprint)
**Status:** proposed assembly draft for review only; not accepted, not implemented, not deployed
**Claim worker:** hermes-laptop-map-032-auto-20261030; claim commit: e26ec68b5278365ce052503f66a2019dde67510f
**Loop:** assembly, policy 1, cycle 5, step 2; key candidate-assembly-v1-stage-2

## 1. Purpose, scope and evidence status

This file is the MAP-032 deliverable: the ARCHITECTURE MAP part of the candidate blueprint. It consolidates existing proposed component boundaries into a single controller/node/adapter/corporation logical map, including trust/authority, secrets and persistence boundaries. It provides a glossary of core entities and identifiers, a crosswalk between catalogue entries, hardware offers, assignments, operations, backups and restore evidence, and a logical interface table with actor/consent, input fields, output fields, error/idempotency behaviour and audit expectations.

It maps existing contract disagreements to proposed alternatives or explicit unresolved choices. No draft is silently upgraded to baseline; no new audit or generator task is opened; no transport, provider, schema or required default is selected. New logical contracts introduced here are labelled proposed. The output is a candidate for review, not accepted work, build-ready certification, implementation or deployment.

Evidence status: all inputs are frozen at pinned revisions. The four baseline documents are user-intent baseline with no upstream technical verification. The MAP-001 through MAP-015 drafts and MAP-017 through MAP-027 follow-ups are unaccepted completed drafts for review only; they are synthesis material, not accepted requirements or verified technical evidence. The blueprint-005.json audit is used for gap context only; its embedded queue proposals are ignored. Genuinely verified evidence is empty.

## 2. Pinned input inventory

| Revision | Paths | Evidence type | Source task |
|---|---|---|---|
| 792b158838aa5214d0156690d24e21e780de542e | README.md; docs/CONCEPT.md; docs/DECISION-GUIDE.md; docs/TRUST-AND-RECOVERY.md | User-intent baseline; no upstream technical verification | — |
| c6cc2de20805455eb55c0343394d01225ff41ffd | docs/map/specs/requirements.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-001 |
| 3585afed129ad2694660fcee8cfd982092551117 | docs/map/specs/permissions.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-002 |
| 0e60848ccbfa295169422eab063f1b81023b390e | docs/map/specs/hosting-assignment.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-003 |
| ccf0957af0d80fe4608fc08b06b02408b485b1ca | docs/map/specs/backup-recovery.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-004 |
| 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 | docs/map/specs/catalogue-entry.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-005 |
| 111a5832102570811dd0af21fffd16a70413febc | docs/map/specs/operations.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-006 |
| 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 | docs/map/specs/scheduling.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-007 |
| 119bb89f6decab9c887e0e99bde38e7d6b1a6744 | docs/map/specs/evidence-record.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-011 |
| 39981db00918b363bc50f33cdb2dfe2dec22d210 | docs/map/specs/node-lifecycle.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-014 |
| 1cd788bd77c027a6808c3c4179784a77d8ca1efe | docs/map/specs/release-lifecycle.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-015 |
| 552d40b359af110eb85e67f58b774de80f2b5cf8 | docs/map/specs/loop-map-017-followup.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-017 |
| 41c48febc50f58304a164ebc4abe174e891193ee | docs/map/specs/loop-map-019-followup.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-019 |
| 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 | docs/map/specs/loop-map-023-followup.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-023 |
| 57dfe172304d5fcf2f19a98f3c16ccbd57131442 | docs/map/specs/loop-map-025-followup.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-025 |
| d45c7a945523ca05447cf8f9757b171fd319b5da | docs/map/specs/loop-map-026-followup.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-026 |
| 6b4aa91aebf4c07de0a9c239ad0b07eb0f6da2de | docs/map/specs/loop-map-027-followup.md | UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence | MAP-027 |
| 4e3dec35f8da85e6fb2668550fe592368a31fc22 | production/proposals/blueprint-005.json | COMPLETED UNACCEPTED AUDIT FOR GAP CONTEXT ONLY; ignore its old queue proposals; no verified technical evidence | MAP-030 |

Blocked prior part: MAP-031 stage 1 — coordination status only, not supplied; task inference budget exhausted; saved work retained; never consumed as evidence.

## 3. Assembly method and fixed stages

The four fixed stages are: (1) build sequence and requirement traceability, (2) component/data/interface map, (3) acceptance/evidence matrix with source pins and open decisions, (4) consolidated candidate blueprint and review handoff. This file is the stage-2 map. Stages 1–3 use the same frozen immutable completed submissions and baseline; stage 4 reads only completed, released assembly parts. MAP-031 is blocked and listed explicitly; it is not consumed as evidence. Queue proposals embedded in older audits are historical gap context only and are not admitted.

## 4. Component/trust map (logical)

**Corporation** — the EVE corporation and its people: CEO, appointed managers, hardware owners, members, recovery custodians (TRUST-AND-RECOVERY.md, "Proposed roles"; CONCEPT.md, "Proposed journey"). The corporation establishes administration and recovery contacts before assignments (REQ-01).

**Controller** — the platform itself. It needs reliable storage and hosting of its own; it presents the catalogue, records offers, proposes assignments and tracks operations. Existing workloads should keep running during controller outages subject to their own dependencies; this must be tested (CONCEPT.md, "Deployment choices"). Automatic failover is a later capability requiring its own evidence (TRUST-AND-RECOVERY.md). Controller resilience is must-be-tested baseline intent, not an implemented feature.

**Node/host** — a volunteered computer, VM or limited resource allocation offered by a hardware owner. The node/offer concept comes from CONCEPT.md ("Members offer a computer, virtual machine or limited resource allocation..."). The eight lifecycle states offered → enrolment-pending → approved → active → disconnected → draining → revoked → retired come only from the MAP-014 draft section 2 and are proposed schema. Management-access removal (revocation) is distinct from verified workload/data cleanup (MAP-014 section 6; MAP-026). An offline host cannot make a new backup; recovery may lose changes since the most recent usable copy.

**Adapter** — application-specific logic for deployment, movement, backup capture and restore verification. Placement considers databases, background jobs, persistent data and application-specific requirements (CONCEPT.md, "Dependency awareness"). Adapters are distinct from the controller and are not selected here.

Trust/authority boundaries:
- CEO appoints managers and recovery custodians; approves critical policy (TRUST-AND-RECOVERY.md).
- Appointed managers manage only explicitly delegated applications and assignments.
- Hardware owner consents to workloads within its offer and may revoke future hosting; revocation affects future hosting and does not by itself undo an in-flight assignment or promise instant deletion on an offline machine (MAP-003 draft, section 5).
- Deployment authority and permission to decrypt backups are separate; CEO succession must not silently grant access to every historical secret. Who may decrypt is unresolved (OD-11; MAP-002 section 3).

Secrets and persistence boundaries:
- Backup encryption keys are managed separately from encrypted copies (baseline must; MAP-004/MAP-005; key-management implementation unresolved).
- Verified copy (backup integrity at rest) is distinct from restore-tested (restore exercise result); one does not imply the other (MAP-004 sections 2 and 6; MAP-027 audit confirmed no conflation).
- Proposed logical split, not established by any supplied input: controller storage holds catalogue, offer, assignment and operation records; node storage holds workload runtime data. Sourced baseline statements retained separately: the controller needs its own reliable storage/hosting (CONCEPT.md, "Deployment choices"); host owners retain the ability to inspect runtime data, so sensitive tokens and authoritative databases should use appropriately trusted infrastructure (TRUST-AND-RECOVERY.md, "Hardware boundaries").

## 5. Glossary of core entities and identifiers

| Entity / identifier | Definition | Source | Status |
|---|---|---|---|
| corporation | EVE corporation administering the platform | baseline (README/CONCEPT) | baseline |
| CEO | appoints managers and recovery custodians; approves critical policy | TRUST-AND-RECOVERY.md | baseline |
| appointed manager | manages explicitly delegated applications and assignments only | TRUST-AND-RECOVERY.md | baseline |
| hardware owner | offers resources, sets limits, consents to workloads, may revoke future hosting | TRUST-AND-RECOVERY.md | baseline |
| member | uses applications to which they are granted access | TRUST-AND-RECOVERY.md | baseline |
| recovery custodian | retrieves or restores specifically authorised recovery material | TRUST-AND-RECOVERY.md | baseline |
| controller | the platform itself; needs its own reliable storage and hosting | CONCEPT.md | baseline |
| node / host | volunteered computer, VM or limited resource allocation | CONCEPT.md | baseline |
| node / host — eight lifecycle states | offered → enrolment-pending → approved → active → disconnected → draining → revoked → retired | MAP-014 section 2 | proposed schema |
| adapter | application-specific deployment, movement, backup capture and restore verification logic | CONCEPT.md (dependency awareness) | proposed |
| catalogue entry | reviewed application bundle; standalone-application / add-on / shared-service | MAP-005 section 4; CONCEPT.md | proposed schema |
| hardware offer | owner's recorded statement of resources, permitted workloads, availability, expiry, movement window, backup-policy reference | MAP-003 section 3 | proposed schema |
| hosting assignment | manager's proposal to run an application version on an approved host within owner consent | MAP-003 section 4 | proposed schema |
| operation | deploy, backup, move, recovery etc. with lifecycle states requested/authorised/queued/running/verifying/completed/failed/cancelled/recovery-required | MAP-006 section 3 | proposed schema |
| backup operation | Requested / Running / Verified copy / Failed | MAP-004 section 2 | proposed schema |
| restore exercise | attempted / succeeded / failed / not performed; separate from backup | MAP-004 section 5; MAP-027 | proposed schema |
| offer_id, assignment_id, entry_id, operation_id, copy_id, exercise_id | locally assigned identifiers | MAP-003/MAP-005/MAP-006/MAP-004 | proposed |

## 6. Entity relationship crosswalk

| From | To | Relationship | Source | Status |
|---|---|---|---|---|
| catalogue entry | hosting assignment | bundle_role (standalone-application / add-on / shared-service) and dependencies must be consistent with the assignment's placement constraints; catalogue entries are not offers themselves | MAP-005 section 4; MAP-003 section 4 | proposed |
| hardware offer | hosting assignment | assignment.offer_id references an existing offer_id; resource_limits must not exceed offer resources; workload within consent_scope | MAP-003 sections 3–4 | proposed |
| hosting assignment | operation | each assignment action (deploy, move, backup, restore) is an operation with actor/consent and a lifecycle state | MAP-006 section 3; MAP-002 section 3 | proposed |
| operation | backup/restore | backup operations use MAP-004 outcome labels; restore exercises are separate evidence items; restore_verified never derived from backup upload | MAP-004 sections 2 and 6; MAP-005 section 9; MAP-027 | confirmed separation; proposed record shapes |
| catalogue entry | restore evidence | restore_exercise and restore_verified are distinct catalogue fields; a GitHub listing alone proves nothing | MAP-004 sections 2, 5 and 6; MAP-005 sections 4.6 and 9 | proposed |
| hardware offer | backup/restore policy reference | backup_policy_ref refers to the owner-accepted policy covering hosted workloads; the separate policy/evidence record is not owned by the offer | MAP-003 section 3 field 9; MAP-004 sections 2 and 6 | proposed |

OD-14: retention and exact times for assignment record fields remain undecided; retention is assignment-level in MAP-003 but targets are unresolved.

## 7. Logical interface operations

| Operation | Actor / consent | Input fields (proposed) | Output fields (proposed) | Error / idempotency | Audit expectation |
|---|---|---|---|---|---|
| Offer hardware | Hardware owner; own offer | offer_id, owner_id, consent_scope, resources, availability, movement_window, expiry, backup_policy_ref, timestamps | Offer record; consent_status active | Invalid offer must not be assigned; no new assignments after revocation | Offer creation/revision with actor and time (MAP-003 section 3) |
| Create assignment | CEO or appointed manager within delegation; hardware owner consent | assignment_id, offer_id, application, version, dependencies, resource_limits, operating_schedule, assignment_expiry, movement_window, destination, backup schedule/policy_ref, retention, recovery_custodian, consent_confirmed_* | Assignment record; case state valid/invalid/withdrawn/offline | Invalid assignments must not be deployed; re-consent default unresolved | Consent timestamps and actor; assignment creation logged (MAP-003 sections 4–5) |
| Deploy | CEO or appointed manager; hardware owner consent and limits | assignment_id, reviewed immutable version, deployment_steps | Deployment record; verifying state | Launch is not success; verification required; duplicate writers forbidden | Verification outcome recorded; citation to procedure version (MAP-006 sections 3/6.1; TRUST-AND-RECOVERY.md) |
| Request backup | Authorised user or scheduler; same procedure for manual/scheduled | operation_id, source manual/scheduled, target application/host, procedure version | Operation record; Requested/Running/Verified copy/Failed | Host offline → Failed; completion/failure recorded; keys separate from encrypted copies | Every backup logged; integrity evidence separate from restore (MAP-004) |
| Retrieve encrypted copy | Recovery custodian; specifically authorised recovery material only | copy_id, custodian authorisation | Encrypted-copy retrieval record | Access limited to authorised material | Custodian and authorised material recorded (TRUST-AND-RECOVERY.md; MAP-002) |
| Decrypt | Not assigned in baseline | Unresolved — who may decrypt and under what rules | Decryption record | Permission separate from deployment authority | Decryption access audited separately (MAP-002; OD-11) |
| Restore | Recovery custodian on a prepared target | exercise_id, source copy id, target, steps performed | Restore exercise record; attempted/succeeded/failed/not performed | Failed restore is a visible failure; isolated restore must not disrupt live routing/writers | Exercise result, custodian, data loss since most recent usable copy, time to recover (MAP-004 section 5) |
| Move assignment | CEO or appointed manager; destination consent and compatibility | assignment_id, destination host, movement window, reviewed version | Move operation; verifying state; rollback on failure | Fence previous writer before new writes; never two authoritative writers merely because both hosts appear healthy; idempotency key | Quiesce, capture/hand over, verify, route change, fence; rollback reason/procedure/outcome recorded (TRUST-AND-RECOVERY.md; MAP-006 section 6.3) |
| Revoke future hosting | Hardware owner; own offer | offer_id, revocation time | consent_status revoked; case state withdrawn | Affects future hosting; existing workload handling unresolved | Revocation recorded with actor/time; no instant-deletion promise (MAP-003 section 5; Example D) |
| Withdraw while offline | Hardware owner; machine already offline | offer_id, disconnection date | Disconnected state retained until cleanup initiated | Offline host cannot make a new backup; recovery may lose changes | Disconnection date noted; cleanup separate from revocation (MAP-014 section 4) |

Idempotency note: any retried operation must support an idempotency key; retrying with the same key must not produce duplicate authoritative effects. For moves this is critical because two authoritative writers must never be admitted merely because both hosts appear healthy. Whether keys are caller-supplied, platform-generated or both is unresolved (MAP-006 section 5.2).

## 8. Contract disagreements and unresolved choices

- MAP-014 section 5 listed a tested restore exercise as required before node offered→approval, presented as baseline-derived. MAP-023/MAP-026 propose replacement wording: enrolment requires hardware owner consent, application reviewed immutable version and measured resources only; demonstrated recoverability is assignment-readiness/owner-policy, explicitly proposed, not baseline-mandated. This map carries the replacement as proposed design and retains the baseline restore-exercise-for-recoverability rule intact; restore-before-approval is not adopted as baseline.
- REQ-16 (repeatable rollout to a second corporation) is unsourced: no baseline section supports it. Retained explicitly as proposed-design/unsourced-only; no modality, section or feasibility invented (MAP-025).
- Decryption authority: separated from deployment authority in baseline; who may decrypt and under what rules is unresolved (OD-11; MAP-002 section 3).
- CEO succession, emergency access and delegation bounds: exact rules are design decisions; succession must not silently grant access to every historical secret (OD-02, OD-10; MAP-002 section 6).
- Volunteer-host workload acceptability vs trusted infrastructure: unresolved (OD-03; TRUST-AND-RECOVERY.md, "Hardware boundaries").
- OD-01: who operates and pays for the central controller — unresolved (DECISION-GUIDE.md, "Questions still open").
- Operating system, deployment runtime, cloud provider, spending-limit enforcement: unselected (OD-04, OD-05).
- Recovery time and data-loss targets per application: unresolved (OD-06).
- Hardware-owner withdrawal while offline: unresolved (OD-07).
- Data-reader consent documentation: unresolved (OD-08).
- Product licensing and distribution model: unresolved (OD-09); no reuse licence selected for this material (README.md, "Project boundaries").
- Automatic failover: later capability requiring its own evidence; not assumed (OD-13; TRUST-AND-RECOVERY.md).
- Cloudflare: optional access and backup component only, not a complete deployment manager; provider selection and feature suitability unverified.
- Retention and exact assignment times: undecided (OD-14; MAP-001 REQ-08 note).

Each unresolved item remains labelled unresolved; no example upgrades an unresolved policy into a mandate.

## 9. Offline and controller-outage limits

- An offline host cannot make a new backup; a missed scheduled backup is not retried silently; catch-up, if any, must be explicit and logged (MAP-007 section 3.4; TRUST-AND-RECOVERY.md).
- Recovery may lose changes since the most recent usable copy; backup is not a live standby (TRUST-AND-RECOVERY.md; MAP-004 section 3).
- Controller outage: existing workloads should keep running during controller outages subject to their own dependencies; this must be tested, not assumed (CONCEPT.md, "Deployment choices"; MAP-004 rule 7). Controller resilience is must-be-tested baseline intent, not an implemented feature; automatic failover is excluded as a later capability.
- Offline revocation: withdrawal is recorded; what happens to running workloads (stop/finish/rollback) requires application-specific fencing and failure tests plus authorised actors; no instant deletion or write-fencing mandate on an offline owner machine (MAP-003 section 5; Example D).
- Movement fencing tolerates clock skew between hosts; wall-clock comparison alone must not decide which writer is authoritative (MAP-007 section 3.5).

## 10. Deployment versus decryption authority

Deployment authority (CEO or appointed manager within delegation, with hardware owner consent) is separate from permission to decrypt backups (not assigned in baseline; who may decrypt is unresolved). Recovery custodian retrieves or restores specifically authorised recovery material; separation of privileges does not require two different people; final role policy is undecided (MAP-003 section 2). CEO succession must not silently grant access to every historical secret. This map preserves the boundary and marks decryption rules as unresolved; no key store, algorithm or assignee is selected.

## 11. Limitations and provenance

- No upstream identity, version or licence is verified for any catalogue candidate (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures, CorpTools); a GitHub listing alone proves none of these.
- No component, integration, restore or cost test exists in the supplied inputs and none is claimed.
- No transport, provider, schema, runtime or required default is selected here.
- No implementation, deployment, access grant or cost is authorised by this task.
- All file citations use pinned revisions listed in Section 2; exact source sections are cited per row.
- Board state and file SHAs were not independently verified; no GitHub, terminal, network or delegation tools are available.
- OD-01 remains unresolved: who operates and pays for the central controller is an open baseline decision (DECISION-GUIDE.md, "Questions still open"); it is not resolved by this map.

## 12. Acceptance criteria mapping

| Acceptance criterion | Location in this file |
|---|---|
| Navigable component/trust map with exact source provenance | Section 4 with per-boundary source citations |
| Entity relationship crosswalk between catalogue entries, hardware offers, assignments, operations, backups and restore evidence | Section 6 |
| Logical interface table with actor/consent, input/output fields, error/idempotency, audit expectations | Section 7 |
| Baseline/proposed distinctions, consent and deployment/decryption boundaries preserved; contradictions and absent decisions recorded | Sections 4, 8, 10; unresolved items labelled throughout |
| Existing source/evidence and unresolved policy labels carried forward; no implication of acceptance, tests, implementation or deployment | Sections 1, 5, 11 |

*End of specification.*
