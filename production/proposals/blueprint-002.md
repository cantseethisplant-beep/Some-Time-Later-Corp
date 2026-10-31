# Blueprint coverage audit — unaccepted draft

This human-readable view is rendered deterministically from the native Hermes JSON audit. It adds no facts or verification. Independent review remains pending.

Coverage audit of all 13 blueprint areas: 6 draft-complete, 3 gap, 4 blocked. All completed drafts remain unaccepted review material. One independently executable source/modality reconciliation is available now: separate node approval from restore-proof requirements using MAP-014, MAP-004 and TRUST-AND-RECOVERY. Other recorded owner decisions, missing technical evidence and unavailable blocked draft inputs remain unresolved; no build-ready claim.

## Coverage

### requirements: draft-complete
REQ-01 through REQ-17 drafted with consolidation status, modality (may/should/must/intent preserved, no collapse), source provenance, and notes, plus OD-01 through OD-14 enumerated with pinned source sections (MAP-001 draft rev c6cc2de20805455eb55c0343394d01225ff41ffd; MAP-017 consolidation rev 552d40b359af110eb85e67f58b774de80f2b5cf8). Both are unaccepted review material, not accepted requirements or technical evidence. REQ-16 has no baseline source section (unsourced proposal); OD-14 retention and exact times are undecided owner decisions. No runtime or restore evidence exists.
References: MAP-001, MAP-017

### roles: draft-complete
Five roles (CEO, appointed manager, hardware owner, member, recovery custodian) and a seven-action deploy/revoke/move/request backup/retrieve encrypted copy/decrypt/restore matrix mapped to consent and boundaries (MAP-002 rev 3585afed129ad2694660fcee8cfd982092551117). Deployment authority and decryption permission separated; succession, emergency access, and delegation remain unresolved design decisions (OD-02, OD-10, OD-11); MAP-018 blocked on gap-key-roles-001. Draft is unaccepted review material, not authority to grant access.
References: MAP-002

### catalogue: draft-complete
Catalogue-entry schema with required/optional fields, four entry states (candidate to supported-for-specific-environment), evidence conditions, and invalidation triggers (MAP-005 rev 96464d45c5c79db31a82bcb9cf13a1b1b65fb141). Backup/restore evidence kept distinct; restore_verified never derived from backup upload. No upstream identity, licence, or version verified; the worked example is synthetic ([synthetic] placeholders), not evidence. Draft is unaccepted.
References: MAP-005

### upstream-evidence: draft-complete
Five evidence categories (user intent, proposed design, documentation-reviewed, component-tested, integration-tested) kept distinct, with common provenance schema, invalidation triggers, and documentation-reviewed templates (MAP-011 rev 119bb89f6decab9c887e0e99bde38e7d6b1a6744; MAP-019 rev 41c48febc50f58304a164ebc4abe174e891193ee). Genuinely verified evidence is none; every component-tested and integration-tested template is marked not performed; backup creation is never accepted as restore verification. Draft is unaccepted.
References: MAP-011, MAP-019

### data-model: blocked
Coordination-only references: MAP-020. These are pinned-board statuses; the blocked drafts were not supplied or independently reassessed. No supplied data-model input document (MAP-020 is not a MAP-022 input). MAP-020 blocked on gap-key-data-model-001: draft preserves baseline/proposed distinctions and a cross-reference matrix, but two correctable defects remain — section 6 lists the expiry redundancy twice (items 3 and 8 identical) contradicting the claimed consolidated seven-item list, and section 5 Retention wrongly attributes retention to the MAP-003 offer schema when section 4 assigns retention only to MAP-003 hosting assignments (the relationship note 'Appears twice at assignment level' is also wrong). Both issues are fixable from supplied text but preserved for independent correction; no accepted unified data model across catalogue, offers, and assignments.
References: baseline only; no completed task evidence

### interfaces: blocked
Coordination-only references: MAP-021. These are pinned-board statuses; the blocked drafts were not supplied or independently reassessed. No supplied interface input document (MAP-021 is not a MAP-022 input). MAP-021 blocked on gap-key-interfaces-001: draft satisfies the five interface aspects and unresolved markings, but two modality/citation issues remain — IA-02 presents proposed logging fields (source, target, time) as baseline should-modality when baseline supports only same-procedure should and record-completion-or-failure must; IA-01 treats MAP-003-proposed validity conditions (expired offer, missing-field mechanics) as baseline-resolved deploy gates while flagging only the backup-policy reference as proposed. Preserved for independent correction; no accepted interface contract.
References: baseline only; no completed task evidence

### node-security: gap
Eight node lifecycle states (offered, enrolment-pending, approved, active, disconnected, draining, revoked, retired) with consent boundaries; management-access removal explicitly distinguished from verified workload/data cleanup; offline-host revocation mechanics noted (MAP-014 rev 39981db00918b363bc50f33cdb2dfe2dec22d210). Unresolved: identity/key mechanism, offline withdrawal procedure, recovery custodian separation from deployment authority, OS/runtime/cloud scope. Draft is unaccepted; no technical verification. Cross-draft gap verified by the coordinator: MAP-014 section 5 presents restore proof as a required node-approval gate, while MAP-004 sections 5/8 and the baseline discuss restore evidence/recoverability without prescribing that enrolment gate. A supplied-text reconciliation is independently executable and is proposed under node-approval-restore-proof-boundary.
References: MAP-004, MAP-014

### controller: blocked
Coordination-only references: MAP-008. These are pinned-board statuses; the blocked drafts were not supplied or independently reassessed. No supplied controller input document (MAP-008 is not a MAP-022 input). MAP-008 blocked: baseline-vs-proposed modality contradictions remain — section 3.1 states 'the controller outage itself must not stop them' as a hard requirement while register row COO-02 marks the same behaviour as baseline intent; section 4.3 states 'commands ... must not be silently applied' as a categorical prohibition while row COO-05 marks it task-imposed proposed and the paragraph concedes concept silence; section 3.1 adds an unlabeled 'must be recorded per application' recording mandate. Bounded corrections exhausted; preserved for independent correction. Not reassessed here because MAP-008 is not a MAP-022 input. No accepted controller-outage behaviour spec.
References: baseline only; no completed task evidence

### scheduling: draft-complete
Time semantics for instants, durations, windows, and recurrences: UTC storage proposed but unresolved (not mandated), explicit timezones, DST spring-forward/fall-back ambiguity, missed schedules, clock uncertainty, movement-window-versus-migration-promise, and backup-creation/restore-verification distinctness (MAP-007 rev 9f330ee125a04bdd6f5df1338b38c93ff2fe0162). No default timezone, schedule, or retention invented; field ownership remains with MAP-003. Draft is unaccepted.
References: MAP-007

### recovery: gap
Backup operation labels (Requested/Running/Verified copy/Failed) separated from retained-copy status and restore-tested result; behaviour rules (same procedure for manual and scheduled, consistent capture, no live standby, no vendor/encryption choice, planned move, emergency recovery, controller resilience); unresolved values (custodian access, key separation, offline hosts, retention, RTO/RPO); evidence a later restore task must supply (MAP-004 rev ccf0957af0d80fe4608fc08b06b02408b485b1ca). No completed restore test claimed. Draft is unaccepted. Cross-draft gap verified by the coordinator: MAP-014 section 5 presents restore proof as a required node-approval gate, while MAP-004 sections 5/8 and the baseline discuss restore evidence/recoverability without prescribing that enrolment gate. A supplied-text reconciliation is independently executable and is proposed under node-approval-restore-proof-boundary.
References: MAP-004, MAP-014

### operations: draft-complete
Nine operation lifecycle states (requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required); truthful progress reporting, timeout and unknown-outcome handling, error classes, retry and idempotency, never infer success from launch; synthetic cases with undecided policy flagged; MAP-004 boundary preserved (MAP-006 rev 111a5832102570811dd0af21fffd16a70413febc). Default timeouts, retry budgets, and idempotency-key ownership unresolved. Draft is unaccepted.
References: MAP-006

### costs: blocked
Coordination-only references: MAP-013. These are pinned-board statuses; the blocked drafts were not supplied or independently reassessed. No supplied cost input document (MAP-013 is not a MAP-022 input). MAP-013 blocked: native Hermes child failed; inspect local scrubbed log. No cloud spending guardrails, spend-limit enforcement, cost measurement, capacity-exceedance behaviour, or provider selection derivable from MAP-022 inputs alone.
References: baseline only; no completed task evidence

### build-and-acceptance: gap
No supplied input document defines build-and-acceptance records, acceptance matrices, source pins with validity conditions, or a frozen map revision. The completion gate (bounded scope, implementation steps, upstream identity/version/licence resolution, consistent roles/data/hosting/recovery/rollout decisions, component evidence, no build-blocking unknowns, frozen revision) is not evidenced by any MAP-022 input. Cannot be accepted or declared build-ready.
References: baseline only; no completed task evidence

## Proposed follow-ups

### node-approval-restore-proof-boundary: Reconcile node approval and restore-proof requirements
Area: node-security
Write a review-only reconciliation note for MAP-014 section 5 and MAP-004 sections 5 and 8, grounded in the supplied TRUST-AND-RECOVERY baseline. Quote the conflicting passages and provide proposed replacement wording for MAP-014 section 5 that separates node enrolment/approval, assignment readiness and demonstrated recoverability. The baseline requires a restore exercise to prove recoverability but does not prescribe it as a node-enrolment gate. Label any proposed restore-before-approval policy as proposed, not baseline-mandated; leave owner policy unresolved. Preserve backup integrity versus restore verification and distinguish a desired test from performed evidence. Do not edit original drafts, choose policy, implement software or claim a test was performed.
Checks:
- Cite the exact supplied revisions and sections for MAP-014, MAP-004 and TRUST-AND-RECOVERY, with a comparison of baseline intent and the disputed approval gate.
- Provide proposed replacement wording and a source/modality crosswalk: restore-before-node-approval is either explicitly proposed or removed as a claimed baseline gate, while the restore-exercise requirement for proof of recoverability remains intact.
- Keep node enrolment, assignment authorisation, backup integrity and demonstrated recoverability distinct; report all test evidence as unverified/not performed and leave owner policy decisions unresolved.

## Exact blockers
- MAP-008 controller outage behaviour: not a MAP-022 input; blocked; baseline-vs-proposed modality contradictions remain (COO-02 baseline intent vs section 3.1 hard requirement; COO-05 proposed vs section 4.3 prohibition; unlabeled per-application recording mandate). Bounded corrections exhausted; preserved for independent correction.
- MAP-013 cloud scope and spending guardrails: not a MAP-022 input; blocked (native Hermes child failed; inspect local scrubbed log). No spend-limit enforcement, cost measurement, capacity-exceedance behaviour, or provider selection derivable from MAP-022 inputs.
- MAP-020 unified data model: not a MAP-022 input; blocked on gap-key-data-model-001 (expiry duplication items 3/8 vs claimed seven-item list; Retention misattributes MAP-003 offer schema vs section 4 assignment-only retention; wrong relationship note).
- MAP-021 minimal interface contract: not a MAP-022 input; blocked on gap-key-interfaces-001 (IA-02 proposed logging fields mislabelled as baseline should; IA-01 MAP-003-proposed validity conditions mislabelled as baseline-resolved deploy gates).
- MAP-016 prior audit task: status review per coordination snapshot; output paths not confirmed as reused or superseded by MAP-022 outputs; no input document supplied for it.
- Owner decisions unresolved across baseline (OD-01 through OD-14): controller operator/payer; CEO identity/delegation/succession/emergency recovery; volunteer-host workload policy; OS/runtime/cloud provider; spending-limit enforcement; RTO/RPO targets; offline withdrawal mechanics; data-reader consent; product licence/distribution. None may be fabricated.
- Build-and-acceptance: no supplied input defining acceptance records, source-pin validity conditions, frozen map revision, or completion-gate evidence; cannot be accepted or declared build-ready.
