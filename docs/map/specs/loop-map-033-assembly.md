# MAP-033 Candidate Blueprint — Acceptance and Evidence Assembly

Task: MAP-033 — Acceptance matrix, source pins and decision register
Claim commit: 5c762a6795eab82de9cc9a013ea56420b83b1551
Worker: hermes-laptop-map-033-auto-20261030
Output path: docs/map/specs/loop-map-033-assembly.md
Input revision: 792b158838aa5214d0156690d24e21e780de542e
Assembly version: 1; assembly step 3 of four fixed stages
Status: unaccepted candidate assembly for review. Not accepted requirements, not technical evidence, no app implemented or tested. No check is marked passed.

## 1. Purpose and evidence status

This file is stage 3 of the finite four-stage assembly package for MAP-033: (1) build sequence and requirement traceability, (2) component/data/interface map, (3) acceptance/evidence matrix with source pins and open decisions (this document), (4) consolidated candidate blueprint and review handoff. It covers all 13 areas: requirements, roles, catalogue, upstream-evidence, data-model, interfaces, node-security, controller, scheduling, recovery, operations, costs, build-and-acceptance.

Every input is labelled with its actual evidence status. The four concept inputs at revision 792b158838aa5214d0156690d24e21e780de542e... are user-intent baseline only; no upstream technical verification exists. MAP-001 through MAP-015 and MAP-017 through MAP-027 drafts are unaccepted completed drafts for review only; they are not accepted requirements, dependency satisfaction, or verified technical evidence. production/proposals/blueprint-005.json (MAP-030) is gap context only; its old queue proposals are ignored. Genuinely verified evidence is empty: no component, integration, restore, or cost test exists and none is claimed, so no acceptance check may be marked passed.

Blocked prior assembly parts are listed explicitly and never consumed as evidence: MAP-031 stage 1 and MAP-032 stage 2 (task inference budget exhausted; saved work retained). They are coordination-only records, not supplied documents.

New schema choices in this assembly — check IDs (AM-*), matrix structure, decision register format — are proposed design, distinct from baseline user intent, and pending separate acceptance. An unresolved policy never becomes a mandate in examples.

## 2. Immutable source inventory

| Revision | Paths | Evidence type | Source task |
|---|---|---|---|
| 792b158838aa5214d0156690d24e21e780de542e | README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md | User-intent baseline; no upstream technical verification | — (baseline) |
| c6cc2de20805455eb55c0343394d01225ff41ffd | docs/map/specs/requirements.md | Unaccepted completed draft for review only | MAP-001 |
| 3585afed129ad2694660fcee8cfd982092551117 | docs/map/specs/permissions.md | Unaccepted completed draft for review only | MAP-002 |
| 0e60848ccbfa295169422eab063f1b81023b390e | docs/map/specs/hosting-assignment.md | Unaccepted completed draft for review only | MAP-003 |
| ccf0957af0d80fe4608fc08b06b02408b485b1ca | docs/map/specs/backup-recovery.md | Unaccepted completed draft for review only | MAP-004 |
| 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 | docs/map/specs/catalogue-entry.md | Unaccepted completed draft for review only | MAP-005 |
| 111a5832102570811dd0af21fffd16a70413febc | docs/map/specs/operations.md | Unaccepted completed draft for review only | MAP-006 |
| 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 | docs/map/specs/scheduling.md | Unaccepted completed draft for review only | MAP-007 |
| 119bb89f6decab9c887e0e99bde38e7d6b1a6744 | docs/map/specs/evidence-record.md | Unaccepted completed draft for review only | MAP-011 |
| 39981db00918b363bc50f33cdb2dfe2dec22d210 | docs/map/specs/node-lifecycle.md | Unaccepted completed draft for review only | MAP-014 |
| 1cd788bd77c027a6808c3c4179784a77d8ca1efe | docs/map/specs/release-lifecycle.md | Unaccepted completed draft for review only | MAP-015 |
| 552d40b359af110eb85e67f58b774de80f2b5cf8 | docs/map/specs/loop-map-017-followup.md | Unaccepted completed draft for review only | MAP-017 |
| 41c48febc50f58304a164ebc4abe174e891193ee | docs/map/specs/loop-map-019-followup.md | Unaccepted completed draft for review only | MAP-019 |
| 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 | docs/map/specs/loop-map-023-followup.md | Unaccepted completed draft for review only | MAP-023 |
| 57dfe172304d5fcf2f19a98f3c16ccbd57131442 | docs/map/specs/loop-map-025-followup.md | Unaccepted completed draft for review only | MAP-025 |
| d45c7a945523ca05447cf8f9757b171fd319b5da | docs/map/specs/loop-map-026-followup.md | Unaccepted completed draft for review only | MAP-026 |
| 6b4aa91aebf4c07de0a9c239ad0b07eb0f6da2de | docs/map/specs/loop-map-027-followup.md | Unaccepted completed draft for review only | MAP-027 |
| 4e3dec35f8da85e6fb2668550fe592368a31fc22 | production/proposals/blueprint-005.json | Completed unaccepted audit for gap context only; no verified technical evidence | MAP-030 |

This inventory is immutable for this assembly run. Source pins in the matrix cite these exact revisions.

## 3. Acceptance and evidence matrix

Proposed check IDs use prefix AM-. Each check records: area, observable procedure, necessary environment/inputs, expected result, source pin, actual evidence status, owner/action needed, invalidation triggers. Evidence status values: unaccepted draft (not passed), baseline intent only (not verified), gap (no supplied document; no check performed), or empty (no verified evidence). No check is marked passed.

### 3.1 Requirements — AM-REQ-01

- Area: requirements.
- Observable procedure: Cross-check REQ-01 through REQ-17 against baseline source sections; preserve may/should/must/intent exactly; no proposed-design gate presented as baseline must; confirm REQ-16 is flagged explicitly unsourced and REQ-17 keeps split provenance (baseline vs MAP-001 draft wording).
- Necessary environment/inputs: docs/map/specs/requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd (MAP-001); baseline 792b158838aa5214d0156690d24e21e780de542e; loop-map-017 @ 552d40b359af110eb85e67f58b774de80f2b5cf8 and loop-map-025 @ 57dfe172304d5fcf2f19a98f3c16ccbd57131442 for modality audit. Repository text review only; no runtime test.
- Expected result: Traceability record per REQ row: status label, modality, source section; REQ-16 explicitly unsourced; REQ-17 split provenance.
- Source pin: docs/map/specs/requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd; baseline CONCEPT.md / TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e.
- Actual evidence status: Unaccepted draft only; consolidation labels are not acceptance.
- Owner/action needed: Reviewer confirms modality preservation and REQ-16/REQ-17 provenance.
- Invalidation triggers: Change to requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd or any cited baseline section.

### 3.2 Roles — AM-ROLES-01

- Area: roles.
- Observable procedure: Verify five roles (CEO, appointed manager, hardware owner, member, recovery custodian) and the seven-action matrix (deploy, revoke, move, request backup, retrieve encrypted copy, decrypt, restore); confirm deployment authority and decrypt permission are separated; confirm succession, emergency access, delegation unresolved.
- Necessary environment/inputs: docs/map/specs/permissions.md @ 3585afed129ad2694660fcee8cfd982092551117 (MAP-002); docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e.
- Expected result: Role/action matrix with consent conditions, boundaries, explicit unresolved-decisions list; no key store, algorithm, or assignee selected.
- Source pin: docs/map/specs/permissions.md @ 3585afed129ad2694660fcee8cfd982092551117; baseline TRUST-AND-RECOVERY — Proposed roles, Hardware boundaries @ 792b158838aa5214d0156690d24e21e780de542e.
- Actual evidence status: Unaccepted draft only; no unresolved policy mandated in examples.
- Owner/action needed: Reviewer confirms no unresolved policy is mandated.
- Invalidation triggers: TRUST-AND-RECOVERY.md revision change; change to permissions.md role matrix.

### 3.3 Catalogue — AM-CAT-01

- Area: catalogue.
- Observable procedure: Check four entry states (candidate, documentation-reviewed, component-tested, supported-for-specific-environment), required versus optional field groups, and backup/restore evidence as distinct items (restore_verified never derived from backup upload).
- Necessary environment/inputs: docs/map/specs/catalogue-entry.md @ 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 (MAP-005); baseline DECISION-GUIDE catalogue entry requirements @ 792b158838aa5214d0156690d24e21e780de542e.
- Expected result: Schema proposal with field groups, invalidation triggers, synthetic example labelled illustrative; no upstream candidate researched or verified.
- Source pin: docs/map/specs/catalogue-entry.md @ 96464d45c5c79db31a82bcb9cf13a1b1b65fb141, sections 3–9.
- Actual evidence status: Unaccepted draft only; genuinely verified evidence empty.
- Owner/action needed: Reviewer confirms required/optional distinctions preserved; no default stack/licence/cost imposed.
- Invalidation triggers: Upstream repository move, licence change, or pinned version superseded without re-review; dependency or deployment-target change.

### 3.4 Upstream-evidence — AM-EVID-01

- Area: upstream-evidence.
- Observable procedure: Confirm five evidence categories (user intent, proposed design, documentation-reviewed, component-tested, integration-tested) kept distinct and never collapsed; check documentation-reviewed template fields and per-category invalidation trigger patterns.
- Necessary environment/inputs: docs/map/specs/evidence-record.md @ 119bb89f6decab9c887e0e99bde38e7d6b1a6744 (MAP-011); loop-map-019 @ 41c48febc50f58304a164ebc4abe174e891193ee (MAP-019).
- Expected result: Reusable provenance/check-result record schema; intent-to-component-tested progression not automatic; no test claimed performed.
- Source pin: docs/map/specs/evidence-record.md @ 119bb89f6decab9c887e0e99bde38e7d6b1a6744, sections 1–7; loop-map-019 @ 41c48febc50f58304a164ebc4abe174e891193ee, sections 3–6.
- Actual evidence status: Unaccepted draft only; all templates marked not performed.
- Owner/action needed: Reviewer confirms categories remain distinct; no backup record treated as restore verification.
- Invalidation triggers: Source file/section at pinned revision changes; component version, interface, or trust-assumption change; concrete failure contradicting a recorded result.

### 3.5 Data-model — AM-DM-01 (gap)

- Area: data-model.
- Observable procedure: No supplied document unifies catalogue entries (MAP-005 section 4), hardware offers (MAP-003 section 3), and assignments (MAP-003 section 4). Propose only a field cross-reference matrix citing each field's source file, section, revision, and required/optional/proposed marking; do not merge schemas or invent units, defaults, or stack values.
- Necessary environment/inputs: docs/map/specs/catalogue-entry.md @ 96464d45c5c79db31a82bcb9cf13a1b1b65fb141; docs/map/specs/hosting-assignment.md @ 0e60848ccbfa295169422eab063f1b81023b390e.
- Expected result: Structural proposal only; retention at assignment level while exact times and retention targets remain undecided (OD-14).
- Source pin: No unifying source; inputs above. Gap recorded by MAP-030 @ 4e3dec35f8da85e6fb2668550fe592368a31fc22.
- Actual evidence status: Gap — no supplied document; no check performed; cannot pass.
- Owner/action needed: Owner commissions a data-model draft or accepts the structural proposal as unaccepted input.
- Invalidation triggers: Change to MAP-005 section 4 or MAP-003 sections 3–4; decision on OD-14.

### 3.6 Interfaces — AM-IF-01 (gap)

- Area: interfaces.
- Observable procedure: No supplied document defines a minimal interface contract. Propose interface aspects only: deployment authority boundary, backup-verification boundary between MAP-004 and MAP-006, movement authorisation boundary, recovery-access boundary, operation-status reporting boundary; cite supplied sources and preserve may/should/must; select no transport, API surface, or queue.
- Necessary environment/inputs: docs/map/specs/permissions.md @ 3585afed129ad2694660fcee8cfd982092551117; docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca; docs/map/specs/operations.md @ 111a5832102570811dd0af21fffd16a70413febc; docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e.
- Expected result: Interface-aspects draft with citations; no implementation choice selected.
- Source pin: Fragmentary baseline inputs only; gap recorded by MAP-030 @ 4e3dec35f8da85e6fb2668550fe592368a31fc22.
- Actual evidence status: Gap — no supplied document; no check performed; cannot pass.
- Owner/action needed: Owner commissions an interfaces draft or accepts the aspects proposal as unaccepted input.
- Invalidation triggers: Change to any cited boundary source; new interface decision by owner.

### 3.7 Node-security — AM-NS-01

- Area: node-security.
- Observable procedure: Check eight node lifecycle states (offered, enrolment-pending, approved, active, disconnected, draining, revoked, retired) and the preserved distinction between management-access removal and verified workload/data cleanup; confirm enrolment prerequisites are consent, immutable version, and measured resources only; confirm restore-before-approval removed as a claimed baseline gate (per MAP-023/MAP-026 proposed replacement wording, proposed design only).
- Necessary environment/inputs: docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210 (MAP-014); loop-map-023 @ 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 and loop-map-026 @ d45c7a945523ca05447cf8f9757b171fd319b5da (proposed replacement wording only); docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e.
- Expected result: Lifecycle state model with revocation vs cleanup separation clearly preserved; identity/key mechanism and offline withdrawal recorded unresolved.
- Source pin: docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210, sections 2–7.
- Actual evidence status: Unaccepted draft only; no identity or key mechanism chosen; no test performed.
- Owner/action needed: Reviewer confirms the disputed restore-gate is labelled proposed design, not baseline-mandated.
- Invalidation triggers: node-lifecycle.md revision change; baseline trust-evidence statement change; owner decision on restore-gating timing.

### 3.8 Controller — AM-CTL-01 (gap)

- Area: controller.
- Observable procedure: No supplied document covers controller outage behaviour as implemented capability. State controller resilience only as baseline intent: workloads should keep running during controller outages subject to their own dependencies, and this must be tested; automatic failover is a later capability requiring its own evidence; no controller storage, hosting, or provider chosen.
- Necessary environment/inputs: docs/CONCEPT.md — Deployment choices @ 792b158838aa5214d0156690d24e21e780de542e; docs/map/specs/operations.md @ 111a5832102570811dd0af21fffd16a70413febc (recovery-required state fragment).
- Expected result: Controller outage behaviour text marked must-be-tested baseline intent only, not implemented feature.
- Source pin: docs/CONCEPT.md — Deployment choices @ 792b158838aa5214d0156690d24e21e780de542e.
- Actual evidence status: Gap — no supplied document; fragments only; cannot pass.
- Owner/action needed: Owner commissions a controller draft or accepts intent-only statement as unaccepted input.
- Invalidation triggers: CONCEPT.md Deployment choices change; owner decision on controller operator/pay (OD-01).

### 3.9 Scheduling — AM-SCH-01

- Area: scheduling.
- Observable procedure: Check time semantics: UTC storage proposed but unresolved; explicit timezones with IANA zone identifiers; daylight-saving ambiguity (skip/normalize/both occurrences undecided); missed schedules (skip/wait/bounded catch-up undecided); clock uncertainty tolerated in fencing; movement window is a time-based permission, not a migration promise; backup creation distinct from restore verification.
- Necessary environment/inputs: docs/map/specs/scheduling.md @ 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 (MAP-007); baseline docs/CONCEPT.md and docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e.
- Expected result: Time-semantics record with nine unresolved policy questions; no default timezone, schedule, or retention invented.
- Source pin: docs/map/specs/scheduling.md @ 9f330ee125a04bdd6f5df1338b38c93ff2fe0162, sections 2–7.
- Actual evidence status: Unaccepted draft only; no scheduling library or default selected.
- Owner/action needed: Reviewer confirms no example resolves an open policy question.
- Invalidation triggers: scheduling.md revision change; MAP-003 field registry decision on storage convention (UTC/local/both).

### 3.10 Recovery — AM-RCV-01

- Area: recovery.
- Observable procedure: Check backup operation labels (Requested, Running, Verified copy, Failed) versus restore-tested result categories (attempted, succeeded, failed, not performed); confirm a successful upload is not proof of recoverability and a restore exercise is required; confirm backup creation and restore verification are distinct record concepts with restore_verified never derived from backup creation.
- Necessary environment/inputs: docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca (MAP-004); loop-map-027 @ 6b4aa91aebf4c07de0a9c239ad0b07eb0f6da2de (MAP-027 audit confirming separation, no change required).
- Expected result: Recovery outcomes record with roles (recovery custodian), unresolved values (custodian access, key separation, offline hosts, retention, RTO/RPO), and evidence list a later restore task must supply; no restore test performed or claimed.
- Source pin: docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca, sections 2, 5, 6, 8.
- Actual evidence status: Unaccepted draft only; this repository claims no restore test.
- Owner/action needed: Reviewer confirms backup/restore separation preserved throughout; restore-gating remains owner policy, not baseline gate.
- Invalidation triggers: backup-recovery.md revision change; owner decision on acceptable data-loss/recovery targets (OD-06).

### 3.11 Operations — AM-OPS-01

- Area: operations.
- Observable procedure: Check nine operation states (requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required); timeout and unknown-outcome handling without inferring success from launch; retry eligibility (transient only, remaining budget) and idempotency requirements; explicit boundary so MAP-006 does not redefine the MAP-004 backup contract.
- Necessary environment/inputs: docs/map/specs/operations.md @ 111a5832102570811dd0af21fffd16a70413febc (MAP-006); docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca boundary reference.
- Expected result: Operation status and failure-reporting model with unresolved policy flagged (default timeouts, retry budgets, idempotency key ownership, recovery-required SLA); synthetic cases flagged as undecided policy.
- Source pin: docs/map/specs/operations.md @ 111a5832102570811dd0af21fffd16a70413febc, sections 3–5, 8–10.
- Actual evidence status: Unaccepted draft only; no runtime tests exist.
- Owner/action needed: Reviewer confirms MAP-004 boundary is stated and no timeout/retry values are defaulted.
- Invalidation triggers: operations.md revision change; MAP-004 backup contract change; owner decision on timeouts/retry policy.

### 3.12 Costs — AM-CST-01 (gap)

- Area: costs.
- Observable procedure: No supplied document addresses cloud spending guardrails or measured hosting costs. Record unresolved cost questions: who operates and pays for the central controller; how cloud spending limits are enforced and what happens if costs or capacity exceed the plan; REQ-10 notes no cost, provider, or retention targets preset.
- Necessary environment/inputs: baseline docs/DECISION-GUIDE.md — Questions still open @ 792b158838aa5214d0156690d24e21e780de542e; docs/map/specs/requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd (REQ-10).
- Expected result: Cost-scope record listing questions only; no currency amount, provider name, spend limit, or default retention value.
- Source pin: docs/DECISION-GUIDE.md — Questions still open @ 792b158838aa5214d0156690d24e21e780de542e; requirements REQ-10 @ c6cc2de20805455eb55c0343394d01225ff41ffd.
- Actual evidence status: Gap — no supplied document; cannot pass.
- Owner/action needed: Owner commissions a cost draft or accepts question record as unaccepted input.
- Invalidation triggers: DECISION-GUIDE open questions change; owner cost/spending decision.

### 3.13 Build-and-acceptance — AM-BA-01

- Area: build-and-acceptance.
- Observable procedure: Assemble the cross-area acceptance matrix (this section) and source-pin inventory (Section 2); record per-area acceptance-criteria location, source revision, status (draft-complete/gap), and unresolved items; use supplied unaccepted MAP-015 release/rollback stages and Verification Checklist as candidate structure only, never as accepted criteria or performed evidence.
- Necessary environment/inputs: All inputs in Section 2; docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe (MAP-015).
- Expected result: This assembly document with one row per 13 areas; no area accepted without supplied evidence; unresolved items listed, not resolved.
- Source pin: docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe, Verification Checklist; all area pins above.
- Actual evidence status: Unaccepted candidate assembly; genuinely verified evidence empty.
- Owner/action needed: Coordinator/owner review of this draft; acceptance remains with project owner or appointed reviewer.
- Invalidation triggers: Any input revision change; new blocked/failed part; coordinator scope change.

## 4. MAP-015 release/rollback verification context (unaccepted candidate only)

Supplied unaccepted MAP-015 (docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe) defines six release lifecycle stages as proposed design: Proposed Release, Reviewed Release, Approved-for-Environment Release, Deployed Release, Superseded Release, Withdrawn Release. It records dependency changes (previous/new version identifiers, affected bundles, compatibility assessment, data/schema migration steps, change owner and approval date), data/schema migrations (migration required, upstream procedure, backup prerequisites, rollback procedure, estimated data-loss window — none executed or tested), backup prerequisites before any release transition modifying persistent state (consistent recovery package, transit/at-rest protection, integrity verification recorded, upload not proof of recoverability, backup not a live standby, offline host cannot make a new backup, keys separate from encrypted copies), and limits of rollback (planned move steps including quiesce, state handover, destination verification, routing change, fencing of the previous writer before new writes; emergency recovery requires a prepared target and accessible recovery data; two authoritative writers never allowed merely because both hosts appear healthy; recovery may lose changes since the most recent usable copy; no runtime test or universal rollback promise).

Its Verification Checklist (eight items: lifecycle stage identified; dependency-change compatibility documented; migration procedure and backup prerequisites documented; backup taken and integrity verified or no-backup flag recorded; rollback procedure documented and accessible; target environment confirmed; hardware owner consent recorded; appointed manager approval recorded) is carried forward strictly as an unaccepted candidate checklist. It is not accepted acceptance criteria, and no item is evidence that any check was performed. Completion of every item is not required for all transitions; unresolved items are flagged, not resolved. One complete deployment and recovery demonstration remains a later adapter-specific evidence need.

## 5. Backup creation versus restore exercise (distinct throughout)

This assembly preserves the separation audited by MAP-027 across MAP-004, MAP-005, MAP-011, MAP-019, and MAP-023: no supplied draft derives restore verification from backup creation, upload success, or integrity-check success.

- Backup creation: an operation produces a consistent recovery package, protects it in transit and at rest, verifies integrity, and records completion or failure. Operation labels are Requested, Running, Verified copy, Failed. A successful upload is not proof of recoverability.
- Restore exercise: a separate operation with result categories attempted, succeeded, failed, not performed. Evidence required: source input revision, restore procedure version, verified copy used, restore target, destination consent/compatibility evidence for moves, steps performed, observed result including data loss since the most recent usable copy and time to recover, custodian, and confirmation no two authoritative writers were admitted (cutover only). A failed restore leaves a visible failure and no success certification; it does not overwrite existing verified-copy evidence.

This repository claims no completed restore tests. Restore-gating of enrolment or approval is explicitly not a baseline requirement; any restore-before-approval policy is proposed design only (per MAP-023/MAP-026 replacement wording) and remains an unresolved owner decision.

## 6. Decision register (unresolved, carried not resolved)

Open questions are pinned to supplied sources. "Alternatives actually stated" lists only options the baseline names; where the baseline asks a question without options, none are listed. "Can planning continue?" distinguishes drafting (yes, with the question marked unresolved) from the completion gate (no, genuine owner decisions and evidence remain blockers).

| ID | Open question | Alternatives actually stated | Affected build steps | Can planning continue without answer? |
|---|---|---|---|---|
| OD-01 | Who operates and pays for the central controller? | Volunteer hardware; trusted server/cloud; hybrid cloud (CONCEPT.md deployment modes) | Costs, controller, build-and-acceptance | Yes for drafting; no for build-ready |
| OD-02 | How are CEO identity, delegation, succession, emergency recovery established? | None stated | Roles, node-security, recovery | Yes for drafting; no for acceptance |
| OD-03 | Which workloads are acceptable on volunteer hosts vs trusted infrastructure? | Volunteer hardware vs trusted server/cloud (decision-guide choice matrix) | Node-security, catalogue, recovery | Yes for drafting |
| OD-04 | Which OS, deployment runtime, cloud provider for the pilot? | None stated | Data-model, interfaces, controller, costs | Yes for drafting |
| OD-05 | How are cloud spending limits enforced; over-capacity behaviour? | None stated | Costs, controller | Yes for drafting |
| OD-06 | Acceptable recovery time and data-loss targets per application? | None stated | Recovery, operations, catalogue | Yes for drafting; no for acceptance |
| OD-07 | How does a hardware owner withdraw while offline? | None stated | Node-security, operations | Yes for drafting |
| OD-08 | Who may read each corporation data type; how is consent documented? | None stated | Roles, catalogue | Yes for drafting |
| OD-09 | Product licensing and distribution model? | None stated | Catalogue, build-and-acceptance | Yes for drafting |
| OD-10 | CEO succession, emergency recovery, delegation rules; succession must not silently grant historical secrets | None stated | Roles, node-security | Yes for drafting |
| OD-11 | Decryption authority separate from deployment; who may decrypt? | None stated | Roles, recovery | Yes for drafting |
| OD-12 | Cloud networking/storage/scheduling/hosting separate; Cloudflare optional only; provider unverified | Cloudflare discussed as optional component | Interfaces, controller | Yes for drafting |
| OD-13 | Automatic failover is a later capability requiring evidence | None stated | Recovery, controller | Yes for drafting |
| OD-14 | Retention and exact times for assignment fields | None stated | Data-model, build-and-acceptance | Yes for drafting |

No unresolved policy is converted into a mandate in this document or its examples.

## 7. Limitations and review pending

- No GitHub, terminal, network, or delegation tools available; board state and file SHAs not independently verified.
- Genuinely verified evidence is empty: no component, integration, restore, or cost test exists or is claimed. No check in this matrix is marked passed.
- All inputs are user-intent baseline or unaccepted completed drafts; nothing here is accepted, merged, deployed, or certified build-ready.
- No owners, dates, costs, stack, licences, providers, or tests are invented.
- Blocked prior assembly parts MAP-031 stage 1 and MAP-032 stage 2 remain coordination-only and are never consumed as evidence.
- Remaining work: stage 4 consolidated candidate blueprint (reads only completed, released assembly parts); coordinator/owner review of this draft (up to two document corrections per task policy); unresolved decisions stay precise prerequisites.

Review pending: yes — coordinator/owner review required; nothing is self-accepted.
