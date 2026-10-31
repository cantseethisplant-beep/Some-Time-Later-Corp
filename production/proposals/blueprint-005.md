# Blueprint coverage audit — unaccepted draft

This human-readable view is rendered deterministically from the native Hermes JSON audit. It adds no facts or verification. Independent review remains pending.

Blueprint coverage audit across all 13 areas for MAP-030. Eight areas have supplied unaccepted drafts (requirements, roles, catalogue, upstream-evidence, node-security, scheduling, recovery, operations); five areas are gaps with no supplied draft (data-model, interfaces, controller, costs, build-and-acceptance). Genuinely verified evidence is empty: no component, integration, restore or cost test exists in the supplied inputs and none is claimed. Six independent follow-up drafting tasks are proposed, each answerable from supplied immutable sources with citations and preserved modality. No area is accepted or treated as build-ready; all owner decisions and upstream verifications remain blockers. Coordinator correction: operations and build-and-acceptance coverage include the supplied MAP-015 release/rollback draft and Verification Checklist as unaccepted candidate inputs, with no area status or acceptance/evidence promotion.

## Coverage

### requirements: draft-complete
MAP-001 draft (docs/map/specs/requirements.md @ c6cc2de2) unifies REQ-01..REQ-17 with status, modality, source provenance and an observable behavioural check per row; MAP-017 follow-up (loop-map-017-followup.md @ 552d40b3) consolidates modalities without collapsing may/should/must and lists OD-01..OD-14 unresolved; MAP-025 (loop-map-025-followup.md @ 57dfe172) retains REQ-16 as explicitly unsourced with no baseline section. Drafts are unaccepted review material, not accepted requirements; retention and exact assignment times remain undecided (OD-14).
References: MAP-001, MAP-017, MAP-025

### roles: draft-complete
MAP-002 draft (docs/map/specs/permissions.md @ 3585afed) defines five roles and a seven-action matrix with required consent, conditions and boundaries; deployment authority and decrypt permission separated as proposed; CEO succession, emergency access and delegation explicitly unresolved (section 6). No key store, algorithm or assignee invented. MAP-018 is blocked on the coordination board (gap-key-roles-001) but its document is not a supplied input; coordination-only status only.
References: MAP-002

### catalogue: draft-complete
MAP-005 draft (docs/map/specs/catalogue-entry.md @ 96464d45) defines four entry states, required versus optional field groups, backup and restore evidence as distinct items with restore_verified never derived from backup upload, invalidation triggers and a synthetic example labelled illustrative. No upstream candidate researched; no stack, licence, cost or default imposed.
References: MAP-005

### upstream-evidence: draft-complete
MAP-011 (docs/map/specs/evidence-record.md @ 119bb89f) and MAP-019 (loop-map-019-followup.md @ 41c48fe) define five evidence categories kept distinct, a documentation-reviewed template with full provenance fields, invalidation trigger patterns per category, and an intent-to-component-tested progression that is not automatic. Genuinely verified evidence is empty; no component, integration, restore or cost test is claimed.
References: MAP-011, MAP-019

### data-model: gap
No supplied document unifies the data model across catalogue entries (MAP-005 section 4), hardware offers (MAP-003 section 3) and assignments (MAP-003 section 4). Coordination board records MAP-020 blocked (gap-key-data-model-001) but that document is not a supplied input, so no independent reassessment or correction is possible from this audit.
References: baseline only; no completed task evidence

### interfaces: gap
No supplied document defines the minimal interface contract from stated intent. Coordination board records MAP-021 blocked (gap-key-interfaces-001) but its document is not supplied; baseline fragments exist in the MAP-002 role/action matrix, MAP-004 sections 2 and 5, and MAP-006 section 8 boundary, none of which constitute an interface contract.
References: baseline only; no completed task evidence

### node-security: draft-complete
MAP-014 (docs/map/specs/node-lifecycle.md @ 39981db0) defines eight node lifecycle states and preserves management-access removal versus verified workload and data cleanup as distinct. MAP-014 section 5's restore-before-approval gate is not baseline; MAP-023 (loop-map-023-followup.md @ 810cc1f9) and MAP-026 (loop-map-026-followup.md @ d45c7a94) propose removing it as a claimed baseline gate, proposed design only and not accepted. No identity or key mechanism chosen; offline withdrawal unresolved.
References: MAP-014, MAP-023, MAP-026

### controller: gap
No supplied document covers controller outage behaviour. Baseline intent in CONCEPT.md Deployment choices (workloads should keep running during controller outages subject to dependencies; must be tested), TRUST-AND-RECOVERY.md (automatic failover a later capability) and ops.md recovery-required state exists only as fragments. Coordination board records MAP-008 blocked but its document is not supplied; coordination-only status only.
References: baseline only; no completed task evidence

### scheduling: draft-complete
MAP-007 draft (docs/map/specs/scheduling.md @ 9f330ee1) defines time semantics: UTC storage proposed but unresolved, explicit timezones, daylight-saving ambiguity, missed schedules, clock uncertainty, movement window versus migration promise, and backup creation distinct from restore verification. Nine policy questions listed unresolved; no default timezone, schedule or retention invented.
References: MAP-007

### recovery: draft-complete
MAP-004 (docs/map/specs/backup-recovery.md @ ccf0957a) defines operation labels Requested, Running, Verified copy and Failed, restore-tested as a separate result category, and evidence a later restore task must supply; no restore test performed or claimed. MAP-027 (loop-map-027-followup.md @ 6b4aa91a) audited thirteen section checks across five drafts and confirmed backup/restore separation with no change required.
References: MAP-004, MAP-027

### operations: draft-complete
MAP-006 draft (docs/map/specs/operations.md @ 111a5832) defines nine operation states, timeout and unknown-outcome handling, retry eligibility and idempotency requirements, synthetic cases, and an explicit boundary so it does not redefine MAP-004's backup contract. Unresolved policy flagged: default timeouts, retry budgets, idempotency key ownership and recovery-required SLA. Supplied unaccepted MAP-015 (docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe) adds proposed release lifecycle stages, dependency-change and data/schema-migration recording, backup prerequisites, limits of rollback, and release/rollback reporting/verification context. These are planning proposals, not performed checks or accepted deployment capability.
References: MAP-006, MAP-015

### costs: gap
No supplied document addresses cloud spending guardrails or measured hosting costs. REQ-10 marks cloud recording optional with no enforced spend limit or provider assumed; DECISION-GUIDE open questions include controller operator and pay and spending-limit enforcement. No currency amount, provider, limit or default may be invented. Coordination board records MAP-013 blocked but its document is not supplied.
References: baseline only; no completed task evidence

### build-and-acceptance: gap
A complete cross-area acceptance matrix and source-pin inventory remain to be assembled. Supplied unaccepted MAP-015 (docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe) provides a Verification Checklist and proposed release/rollback lifecycle, dependency/migration recording, backup prerequisites and rollback limitations as candidate acceptance-structure inputs. The checklist is neither accepted acceptance criteria nor evidence that any check was performed. MAP-029 and MAP-012 remain blocked coordination records, not supplied documents.
References: MAP-015

## Proposed follow-ups

### gap-key-data-model-001: Cross-reference catalogue, offer and assignment field inventories
Area: data-model
Draft a field cross-reference matrix from supplied MAP-005 section 4 (catalogue entry fields), MAP-003 section 3 (hardware offer fields) and MAP-003 section 4 (hosting assignment fields), preserving each field's required, optional or proposed marking and source citation. Note retention is assigned at assignment level while exact times and retention targets remain undecided (OD-14). Do not merge the schemas, invent units, defaults, stack values or a shared required field list.
Checks:
- Every matrix row cites its source file, section and revision, for example docs/map/specs/catalogue-entry.md section 4 @ 96464d45
- No field is marked required without a cited source; proposed fields remain labelled proposed and unresolved decisions stay unresolved

### gap-key-controller-001: Draft controller outage behaviour from supplied intent
Area: controller
Draft controller outage behaviour text citing CONCEPT.md Deployment choices (workloads should keep running during controller outages subject to their own dependencies; this must be tested), TRUST-AND-RECOVERY.md (automatic failover is a later capability requiring its own evidence) and ops.md recovery-required state. State controller resilience as must-be-tested baseline intent only, not an implemented feature. Do not assume failover or choose controller storage, hosting or provider.
Checks:
- Controller outage behaviour is stated only as baseline intent with citations to CONCEPT.md and ops.md and marked must-be-tested, not implemented
- Automatic failover is excluded as a later capability requiring its own evidence; no controller storage, hosting or provider is chosen

### gap-key-costs-001: Record unresolved cost and spending-guardrail questions without inventing figures
Area: costs
Draft a cost-scope record listing unresolved cost questions from the baseline: who operates and pays for the central controller, how cloud spending limits are enforced and what happens if costs or capacity exceed the plan, with REQ-10 noting no cost, provider or retention targets preset. Cite DECISION-GUIDE Questions still open and requirements REQ-10. Include no currency amount, provider name, spend limit or default retention.
Checks:
- Each cost question is traced to a supplied source section (DECISION-GUIDE Questions still open; requirements REQ-10)
- No currency amount, provider name, spend limit or default retention value appears anywhere in the draft

### gap-key-build-and-acceptance-001: Propose baseline acceptance matrix structure and source-pin inventory
Area: build-and-acceptance
Draft an acceptance matrix structure covering all 13 blueprint areas; for each area record the acceptance-criteria location in supplied drafts, source revision, status (draft-complete, gap or blocked) and unresolved items. This is a structural proposal only and accepts no area.
Checks:
- Matrix has one row per all 13 areas with acceptance-criteria location, source revision and status
- No row marks an area accepted without supplied evidence; unresolved items are listed, not resolved

### gap-key-roles-001: Record unresolved role authority decisions from supplied baseline
Area: roles
Draft a role-decision record listing explicitly unresolved role decisions pinned to TRUST-AND-RECOVERY.md sections: CEO succession must not silently grant access to every historical secret; emergency access authorised actors, conditions, declarer, duration and audit; delegation bounds including owner-consent gate, no decrypt by default, no appoint or policy authority, CEO revocation, expiry and duration defaults; decryption authority separate from deployment authority with who may decrypt unresolved. Resolve none of them.
Checks:
- Every decision cites TRUST-AND-RECOVERY.md Proposed roles, Hardware boundaries or Backup and movement section
- No succession rule, emergency-access actor or delegation bound is selected, defaulted or treated as resolved

### gap-key-interfaces-001: Draft minimal interface aspects from stated intent with preserved modality
Area: interfaces
Draft interface aspects covering the deployment authority boundary, the backup-verification boundary between MAP-004 and MAP-006, the movement authorisation boundary, the recovery-access boundary and the operation-status reporting boundary. Cite supplied sources (MAP-002 matrix, MAP-004 sections 2 and 5, MAP-006 section 8, TRUST-AND-RECOVERY.md) and preserve may/should/must exactly. Select no transport, API surface, queue or implementation choice.
Checks:
- Each aspect cites its supplied source file and section
- Modality markers are preserved exactly and no implementation choice (transport, API surface, queue) is selected

## Exact blockers
- No upstream identity, version or licence verified for any catalogue candidate (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures, CorpTools); a GitHub listing alone proves none of these.
- Genuinely verified evidence is empty: no component, integration, restore or cost test exists in the supplied inputs and none is claimed.
- Owner decisions unresolved: controller operator and pay (OD-01); CEO identity, delegation, succession and emergency recovery (OD-02/OD-10); volunteer-host workload acceptability (OD-03); OS, deployment runtime and cloud provider (OD-04); cloud spending-limit enforcement and over-capacity behaviour (OD-05); recovery time and data-loss targets per application (OD-06); hardware-owner withdrawal while offline (OD-07); data-reader consent documentation (OD-08); product licensing and distribution model (OD-09); decryption authority separate from deployment, who may decrypt (OD-11); automatic failover evidence (OD-13); retention and exact assignment times (OD-14).
- Automatic failover is not assumed and requires its own evidence (OD-13); Cloudflare is discussed only as an optional access and backup component, not a complete deployment manager, and provider selection and feature suitability remain unverified.
- No supply-versus-demand host measurements, verified restore exercises, or cloud cost figures exist; these are not repaired by inventing facts.
- Board state and file SHAs were not independently verified; no GitHub, terminal, network or delegation tools are available.
