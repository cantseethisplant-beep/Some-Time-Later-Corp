# MAP-034 Candidate Blueprint — CANDIDATE — NOT ACCEPTED OR BUILD-READY

> Coordinator recovery context: this historical candidate was generated before the three detailed assembly parts were published. Its missing/blocked-part statements describe that original input snapshot, not the current board. Newly published corrected parts: MAP-031: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/25 @ f72e9b995af03cd88cc096c0146186595da33f0d; MAP-032: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/26 @ c426a685a2c40bd74a2a4db63acb645d3e210d85; MAP-033: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/27 @ 90c954ddeb85b66508c668039244791a689ce629. A distinct integration task will consume those new immutable inputs; this document does not claim it already did so.


**Status: CANDIDATE — NOT ACCEPTED OR BUILD-READY.** Planning and review document only. No app is implemented, no deployment exists, no restore test has been performed, and no stack, provider, licence, cost, or implementation is selected or certified.

Task MAP-034 · Claim worker hermes-laptop-map-034-auto-20261030 · Claim commit f66ae809ee33d9c3efc06c776780ad42a7441d35 · Assembly version 1, step 4 of four fixed stages · Output path docs/map/specs/loop-map-034-candidate.md

## 1. Navigation index

1. Immutable source inventory (§2)
2. Stage 1 — build sequence and requirement traceability (§3)
3. Stage 2 — component/data/interface map and trust boundaries (§4)
4. Stage 3 — acceptance/evidence matrix, source pins, open decisions (§5)
5. Owner/reviewer decision list (§6)
6. Limitations and builder instructions (§7–§8)

## 2. Immutable source inventory

All source references below are exact, pinned, full 40-character revisions. No abbreviated revision is used anywhere in this document.

Baseline (user intent; no upstream technical verification), revision 792b158838aa5214d0156690d24e21e780de542e:
- README.md
- docs/CONCEPT.md
- docs/DECISION-GUIDE.md
- docs/TRUST-AND-RECOVERY.md

Completed unaccepted drafts (review material only; not accepted requirements, dependency satisfaction, or verified technical evidence):
- MAP-001 docs/map/specs/requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd — REQ-01..REQ-17, OD-01..OD-14
- MAP-002 docs/map/specs/permissions.md @ 3585afed129ad2694660fcee8cfd982092551117 — roles and action matrix
- MAP-003 docs/map/specs/hosting-assignment.md @ 0e60848ccbfa295169422eab063f1b81023b390e — hardware offer and assignment fields
- MAP-004 docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca — backup/restore outcomes
- MAP-005 docs/map/specs/catalogue-entry.md @ 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 — catalogue fields and states
- MAP-006 docs/map/specs/operations.md @ 111a5832102570811dd0af21fffd16a70413febc — operation states
- MAP-007 docs/map/specs/scheduling.md @ 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 — time semantics
- MAP-011 docs/map/specs/evidence-record.md @ 119bb89f6decab9c887e0e99bde38e7d6b1a6744 — evidence categories and provenance
- MAP-014 docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210 — node enrolment/withdrawal
- MAP-015 docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe — release/rollback lifecycle
- MAP-017 docs/map/specs/loop-map-017-followup.md @ 552d40b359af110eb85e67f58b774de80f2b5cf8 — requirement consolidation
- MAP-019 docs/map/specs/loop-map-019-followup.md @ 41c48febc50f58304a164ebc4abe174e891193ee — evidence workflow
- MAP-023 docs/map/specs/loop-map-023-followup.md @ 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 — restore-proof reconciliation
- MAP-025 docs/map/specs/loop-map-025-followup.md @ 57dfe172304d5fcf2f19a98f3c16ccbd57131442 — REQ-16 unsourced row
- MAP-026 docs/map/specs/loop-map-026-followup.md @ d45c7a945523ca05447cf8f9757b171fd319b5da — enrolment gate restatement
- MAP-027 docs/map/specs/loop-map-027-followup.md @ 6b4aa91aebf4c07de0a9c239ad0b07eb0f6da2de — backup/restore separation audit

Gap context only (old queue proposals ignored; no verified technical evidence):
- MAP-030 production/proposals/blueprint-005.json @ 4e3dec35f8da85e6fb2668550fe592368a31fc22 — 13-area coverage audit and gap/task list

Blocked parts (coordination status only; documents not supplied; never consumed as evidence):
- MAP-031 stage 1 — task inference budget exhausted; saved work retained
- MAP-032 stage 2 — task inference budget exhausted; saved work retained
- MAP-033 stage 3 — submitted as a JSON wrapper instead of the required plain-text file sections; reformatting only; substance not admitted as evidence

Missing/gap areas from MAP-030 context (no supplied input, none consumed): data-model (MAP-020), interfaces (MAP-021), controller (MAP-008), costs (MAP-013).

## 3. Stage 1 — build sequence and requirement traceability

### Bounded MVP scope

README.md ("What a first version might cover"): app catalogue, hardware registration, CEO and delegated roles, owner-approved resource limits, one controlled hosting target, scheduled and manual backups with a tested restore. Multiple hosts, service movement, failover, and cloud provisioning are deferred until the foundation is demonstrated. All items below are intent, not implemented features.

### Numbered implementation order (bounded)

1. Record corporation administration and recovery contacts/custodians before any assignment (REQ-01; CONCEPT step 1; TRUST-AND-RECOVERY roles).
2. Capture hardware offers with owner-set resources, availability, permitted workloads, expiry, and backup-policy reference (REQ-02; MAP-003 §3).
3. Manager chooses a reviewed bundle and inspects dependencies/resource requirements; catalogue entry created in candidate state with required identity fields populated or marked unresolved (REQ-03, REQ-14; CONCEPT step 3; MAP-005 §3–4).
4. Create assignments only within owner consent and approved limits, using the required subset (REQ-04, REQ-08; MAP-003 §4). The hard "must not exceed" rejection gate is proposed design (MAP-003 proposed assignability rule), not a baseline mandate; baseline modality is "should".
5. Prepare and verify a controlled deployment on an approved host before use (REQ-05; proposed; CONCEPT step 5).
6. Run manual and scheduled backups through the same application-specific procedure; record completion or failure (REQ-06, REQ-09; MAP-004 §2–3; MAP-006).
7. Execute movement/recovery per application-specific procedure: quiesce writes and jobs, capture or hand over consistent state, verify destination, change routing, fence the previous writer before new writes, tested rollback on failure (REQ-07; TRUST-AND-RECOVERY backup/movement).
8. Handle owner withdrawal and offline hosts: record withdrawal, exclude host from new assignments, no instant-deletion or write-fencing mandate on an offline machine (REQ-17; MAP-003 §5; MAP-014).

### Requirement-to-build-step/check matrix

| REQ | Status | Modality | Source | Build step | Check | Evidence |
|-----|--------|----------|--------|------------|-------|----------|
| REQ-01 | required | intent | CONCEPT step 1; TRUST roles | 1 | Contacts/custodians recorded | baseline intent — unverified |
| REQ-02 | required | may | README idea; CONCEPT step 2 | 2 | Offer lists resources, availability, workloads | baseline intent — unverified |
| REQ-03 | required | intent | CONCEPT step 3 | 3 | Manager selection with dependency/resource summary | baseline intent — unverified |
| REQ-04 | required | should | CONCEPT journey; TRUST hardware boundaries | 4 | Rejected outside offer/limits — gate is proposed design | baseline intent — unverified; proposed-design gate |
| REQ-05 | proposed | intent | CONCEPT step 5 | 5 | Deployment verified before active | baseline intent — unverified |
| REQ-06 | required | may | CONCEPT step 6 | 6 | Health visible; backups logged | baseline intent — unverified |
| REQ-07 | required | intent | CONCEPT step 7 | 7 | Movement/recovery log: outcome + attention items | baseline intent — unverified |
| REQ-08 | proposed | could/may | CONCEPT hosting assignment | 4 | Required fields present; missing blocks creation | unaccepted draft |
| REQ-09 | proposed | should | CONCEPT hosting assignment; TRUST backup/movement | 6 | Manual and scheduled share one procedure | unaccepted draft |
| REQ-10 | proposed | may | README idea; CONCEPT deployment choices | 2 | Cloud entry possible; no spend limit assumed | unaccepted draft |
| REQ-11 | proposed | must | CONCEPT dependency awareness | 3 | Entry type populated before placement | unaccepted draft |
| REQ-12 | proposed | must | CONCEPT dependency awareness | 3, 4 | Placement checks dependency-aware requirements | unaccepted draft |
| REQ-13 | proposed | should not | README first version; project boundaries | — | No duplicate Discord communication | unaccepted draft |
| REQ-14 | proposed | must | DECISION-GUIDE catalogue entry requirements | 3 | All catalogue fields populated | unaccepted draft |
| REQ-15 | proposed | must | TRUST backup/movement; CONCEPT hosting assignment | 6 | Verifiable package; keys separate from copies | baseline intent — unverified |
| REQ-16 | proposed | none claimed — unsourced | none | — | No baseline section; prerequisite: source or owner decision | unsourced |
| REQ-17 | proposed | may | TRUST roles/hardware boundaries | 8 | Withdrawal recorded; host excluded; no instant deletion offline | baseline intent — unverified |

All evidence rows are unaccepted drafts or unverified baseline intent; no runtime or restore evidence exists.

## 4. Stage 2 — component/data/interface map and trust boundaries

### Component/data overview (proposed schemas, pending acceptance)

Catalogue entry (MAP-005 §4): entry_id, upstream_name, upstream_repository, upstream_licence, pinned_version, version_source, maintenance_status, bundle_role, bundle_members, dependencies, placement_constraints, deployment_authority, hardware_consent_required, permitted_workloads, isolation_level, sensitive_data_handling, recovery_custodian, measured_resources, deployment_target, cloud_responsibilities, storage_model, deployment_steps, update_procedure, rollback_procedure, movement_procedure, controller_outage_behaviour, backup_schedule, backup_consistency, backup_integrity, backup_keys_managed_separately, backup_record, restore_exercise, restore_verified, acceptable_data_loss_window. States: candidate, documentation-reviewed, component-tested, supported-for-specific-environment (MAP-005 §3). Backup and restore evidence are distinct items; restore_verified is never derived from backup upload. Every field is a proposed schema rule pending acceptance, not baseline fact.

Hardware offer (MAP-003 §3): offer_id, owner_id, consent_scope, consent_status, resources, availability, movement_window, expiry, backup_policy_ref, offered_at/last_revised_at. Assignable only when all fields present and consent_status active (proposed assignability rule).

Hosting assignment (MAP-003 §4): assignment_id, offer_id, application, version, dependencies, resource_limits, operating_schedule, assignment_expiry, movement_window, destination, backup_schedule/backup_policy_ref, retention, recovery_custodian, proposed_by/proposed_at/consent_confirmed_at/consent_confirmed_by. Required subset: assignment_id, offer_id, application, version, resource_limits, assignment_expiry, recovery_custodian, and at least one of operating_schedule/movement_window.

Operation record (MAP-006 §4): identifier, type, state, actor, target, timestamps, step/stage, progress or "unknown", outcome summary, failure reason/error class, retry count, idempotency key. States: requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required.

Backup/restore records (MAP-004 §6): backup operation record, retained-copy record, restore exercise record. Restore-tested is a separate result category (attempted/succeeded/failed/not performed), not a copy lifecycle state.

### Interface boundaries (no transport, API, or queue selected)

- Deployment authority vs permission to decrypt backups: separate (TRUST-AND-RECOVERY roles; MAP-002 matrix).
- Movement authorisation boundary: destination consent and compatibility, quiesce, fence previous writer before new writes; never two authoritative writers (TRUST-AND-RECOVERY; MAP-015).
- Recovery-access boundary: recovery custodian retrieves/restores specifically authorised material only (TRUST-AND-RECOVERY).
- Operation-status reporting boundary: status reporting only; does not redefine MAP-004 backup contract (MAP-006 §8).

### Trust boundaries

- Node enrolment/approval (offered → approved): hardware owner consent, application reviewed immutable version, measured resources only. Restore-proof is not a baseline enrolment gate; demonstrated recoverability is assignment-readiness/owner-policy, explicitly proposed design (MAP-023 §4 and MAP-026 §4 proposed replacement wording for MAP-014 §5; both unaccepted).
- Controller: needs reliable storage/hosting of its own; workloads should keep running during controller outages subject to dependencies; must be tested (CONCEPT deployment choices). Automatic failover excluded — later capability requiring its own evidence (TRUST-AND-RECOVERY).

### Deployment/update/rollback and backup/restore path

- Release stages (MAP-015): proposed → reviewed → approved-for-environment → deployed → superseded → withdrawn. Dependency changes and data/schema migrations recorded per release; migration steps not executed or tested here.
- Backup prerequisites before state-changing transitions: consistent package, protection in transit/at rest, integrity verification recorded, successful upload ≠ recoverability, keys separate from encrypted copies (MAP-015 backup prerequisites; MAP-004 §3).
- Rollback limits: application-specific; no universal promise; on verification failure stop and use tested rollback; never two authoritative writers merely because both hosts appear healthy (MAP-015; TRUST-AND-RECOVERY).
- Restore: requires prepared target and accessible recovery data; restore exercise required to prove recoverability (MAP-004 §5; TRUST-AND-RECOVERY).

## 5. Stage 3 — acceptance/evidence matrix, source pins, open decisions

### Acceptance matrix across the 13 blueprint areas

| Area | Acceptance-criteria location in supplied drafts | Source revision | Status | Unresolved items |
|------|------------------------------------------------|-----------------|--------|------------------|
| requirements | MAP-001 §6; REQ table §2 | c6cc2de20805455eb55c0343394d01225ff41ffd | draft-complete | OD-01..OD-14; REQ-16 unsourced |
| roles | MAP-002 §6, §7 | 3585afed129ad2694660fcee8cfd982092551117 | draft-complete | CEO succession, emergency access, delegation bounds |
| catalogue | MAP-005 §9; §8 | 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 | draft-complete | upstream identity/version/licence for any candidate |
| upstream-evidence | MAP-011 §7; MAP-019 §8 | 119bb89f6decab9c887e0e99bde38e7d6b1a6744 / 41c48febc50f58304a164ebc4abe174e891193ee | draft-complete | no component/integration/restore/cost test |
| data-model | none supplied | — | gap | cross-reference catalogue/offer/assignment fields (MAP-020 blocked) |
| interfaces | none supplied | — | gap | minimal interface contract (MAP-021 blocked) |
| node-security | MAP-014 §7; MAP-023/MAP-026 proposed corrections | 39981db00918b363bc50f33cdb2dfe2dec22d210 | draft-complete | identity/key mechanism; offline withdrawal |
| controller | baseline fragments only | — | gap | controller outage behaviour as must-be-tested intent only (MAP-008 blocked) |
| scheduling | MAP-007 §7 | 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 | draft-complete | storage convention, DST resolution, missed-schedule policy |
| recovery | MAP-004 §9; MAP-027 §7 | ccf0957af0d80fe4608fc08b06b02408b485b1ca | draft-complete | no restore test performed or claimed |
| operations | MAP-006 §10; MAP-015 checklist as candidate context only | 111a5832102570811dd0af21fffd16a70413febc / 1cd788bd77c027a6808c3c4179784a77d8ca1efe | draft-complete | default timeouts, retry budgets, idempotency key ownership |
| costs | none supplied | — | gap | spending limits, over-capacity behaviour, no figures (MAP-013 blocked) |
| build-and-acceptance | MAP-015 verification checklist as unaccepted candidate context | 1cd788bd77c027a6808c3c4179784a77d8ca1efe | gap | full acceptance matrix and source-pin inventory (this document, stage 3) |

No row marks an area accepted; every area carries unresolved items or is a gap.

### Open decisions (OD-01..OD-14)

OD-01 controller operator and payer; OD-02 CEO identity/delegation/succession/emergency recovery; OD-03 volunteer-host workload acceptability vs trusted infrastructure; OD-04 pilot OS/runtime/cloud provider; OD-05 cloud spending-limit enforcement and over-capacity behaviour; OD-06 recovery time and data-loss targets per application; OD-07 hardware-owner withdrawal while offline; OD-08 data-reader consent documentation; OD-09 product licensing and distribution model; OD-10 exact succession/emergency/delegation rules; OD-11 decryption authority separate from deployment, who may decrypt; OD-12 Cloudflare as optional component only, provider suitability unverified; OD-13 automatic failover evidence; OD-14 retention and exact assignment times. All unresolved; pinned to DECISION-GUIDE/TRUST-AND-RECOVERY via MAP-017 §3.

### Consolidated duplicate note

The restore-proof/enrolment correction appears in both MAP-023 §4 and MAP-026 §4 as proposed replacement wording for MAP-014 §5 — enrolment requires consent, immutable version, and measured resources only; restore-before-approval is removed as a claimed baseline gate and relabelled proposed design. Consolidated once here, cited with both sources; not adopted as policy.

### Build prerequisites (must be resolved before build; none may be invented)

- Upstream identity, version, and licence verified for any catalogue candidate (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures, CorpTools); a GitHub listing proves none of these.
- Measured resources and deployment target (OS, deployment runtime, cloud provider) for the pilot.
- Compatibility/resource measurements for bundles, databases, background jobs, persistent data.
- Restore evidence: at least one restore exercise per supported application; none performed or claimed (MAP-004 §8; MAP-027).
- Owner decisions OD-01..OD-14 and the REQ-16 baseline-source decision.
- Missing parts: MAP-031, MAP-032, MAP-033 (coordination-blocked); data-model (MAP-020), interfaces (MAP-021), controller (MAP-008), costs (MAP-013) gaps — none supplied, none consumed.

## 6. Owner/reviewer decision list

| Decision | Owner | Due | Status |
|----------|-------|-----|--------|
| OD-01..OD-14 (all fourteen) | project owner / appointed reviewer | unresolved | open |
| REQ-16 baseline source or removal decision | project owner / reviewer | unresolved | open |

All decisions are genuine owner choices; this document makes none of them.

## 7. Limitations

- No GitHub, terminal, network, or delegation tools were used; board state and file SHAs were not independently verified.
- Every supplied draft is unaccepted review material; this blueprint is not acceptance, merge, deployment, or build-readiness certification.
- No upstream software identity, version, licence, dependency, cost, component test, integration test, restore test, or runtime test is claimed.
- REQ-16 is retained as explicitly unsourced; no baseline modal verb or source section was invented.
- MAP-033 was noted only as a blocked, non-conforming package; its substance was not consumed as evidence.
- Later reconciliation text (MAP-023, MAP-026) is applied only as unaccepted proposed correction, not automatic supersession of agreed intent.

## 8. Builder instructions

Begin with this map and resolve only the listed blockers and open decisions; do not repeat broad discovery. For each blocked or missing part named above, obtain the supplied input or record why it cannot be supplied before consuming it as evidence. Review pending: yes — acceptance rests with the project owner or an appointed reviewer.
