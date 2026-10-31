# Blueprint coverage audit — unaccepted draft

This human-readable view is rendered deterministically from the native Hermes JSON audit. It adds no facts or verification. Independent review remains pending.

Audit of the usable-blueprint completion gate across 13 areas using the supplied baseline revision 792b158838aa5214d0156690d24e21e780de542e README.md docs/CONCEPT.md docs/DECISION-GUIDE.md docs/TRUST-AND-RECOVERY.md and the supplied unaccepted completed drafts. Coverage is drafting only; no app, tested restore, measured cost, selected stack, or upstream identity verification exists. Five areas are not draft-complete: three blocked (upstream-evidence, controller, costs) and two gaps (data-model, build-and-acceptance). One independent drafting follow-up remains executable from supplied text; no quota-filling tasks are invented. Backup creation and restore verification remain strictly distinct, and no draft is treated as accepted or build-ready.

## Coverage

### requirements: draft-complete
REQ-01 through REQ-17 are consolidated in docs/map/specs/requirements.md at revision c6cc2de20805455eb55c0343394d01225ff41ffd (MAP-001 draft, unaccepted review material only). Modality is preserved row by row in docs/map/specs/loop-map-017-followup.md at revision 552d40b359af110eb85e67f58b774de80f2b5cf8 (MAP-017 draft): may/should/must/intent are not collapsed. REQ-16 is unsourced - no baseline section supports second-corporation rollout - and is preserved as proposed design with no modality invented. Open decisions OD-01 through OD-14 remain unresolved. Draft completeness applies to drafting only; none of these requirements are accepted, verified, or evidence.
References: MAP-001, MAP-017, MAP-025

### roles: draft-complete
Five roles (CEO, appointed manager, hardware owner, member, recovery custodian) and a seven-action role/action matrix are defined in docs/map/specs/permissions.md at revision 3585afed129ad2694660fcee8cfd982092551117 (MAP-002 draft). Deployment authority and permission to decrypt backups are separated; exact CEO succession, emergency access, and delegation rules remain explicitly unresolved in Section 6. Complete draft material awaiting review, not a gap requiring a new drafting task.
References: MAP-002

### catalogue: draft-complete
Catalogue entry schema with required/optional field classification, four entry states (candidate, documentation-reviewed, component-tested, supported-for-specific-environment), evidence conditions, invalidation triggers, and a synthetic unverified example is defined in docs/map/specs/catalogue-entry.md at revision 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 (MAP-005 draft). Backup creation and restore verification are treated as separate evidence items; restore_verified is never derived from backup upload. Candidate names are historical planning context only; no upstream identity, licence, or version is verified.
References: MAP-005

### upstream-evidence: blocked
Evidence categories (user intent, proposed design, documentation-reviewed, component-tested, integration-tested) and documentation-reviewed template records are defined in docs/map/specs/evidence-record.md at revision 119bb89f6decab9c887e0e99bde38e7d6b1a6744 (MAP-011 draft) and docs/map/specs/loop-map-019-followup.md at revision 41c48febc50f58304a164ebc4abe174e891193ee (MAP-019 draft). Genuinely verified evidence: none exists in any supplied input. No component, integration, restore, or cost test has been performed. Blocked because upstream identity, version, licence, and dependency evidence are unavailable from supplied sources and must remain an exact blocker rather than a drafting task.
References: MAP-011, MAP-019

### data-model: gap
Hardware-offer and hosting-assignment field schemas are proposed in docs/map/specs/hosting-assignment.md at revision 0e60848ccbfa295169422eab063f1b81023b390e (MAP-003 draft); catalogue-entry fields are proposed in docs/map/specs/catalogue-entry.md (MAP-005 draft). No cross-area data-model unification exists between offers, assignments, and catalogue entries, and no accepted field registry maps field names, types, or required/optional statuses across schemas. This drafting gap is already tracked on the coordination board by blocked MAP-020 (coordination-only status; its document is not a supplied input), so MAP-028 does not re-propose the same gap key to avoid duplication. The gap remains open for independent correction.
References: MAP-003, MAP-005

### interfaces: draft-complete
Operation states (requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required), timeout and unknown-outcome handling, retry eligibility, idempotency, and synthetic cases are defined in docs/map/specs/operations.md at revision 111a5832102570811dd0af21fffd16a70413febc (MAP-006 draft) with an explicit boundary not redefining the MAP-004 backup contract. Time semantics (UTC storage intent unresolved, explicit timezones, DST ambiguity, missed schedules, clock skew, movement window versus migration promise) are defined in docs/map/specs/scheduling.md at revision 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 (MAP-007 draft). Default timeouts, retry budgets, and idempotency-key ownership remain unresolved policy.
References: MAP-006, MAP-007

### node-security: draft-complete
Eight node lifecycle states (offered, enrolment-pending, approved, active, disconnected, draining, revoked, retired) and the management-access-removal versus verified-workload/data-cleanup distinction are defined in docs/map/specs/node-lifecycle.md at revision 39981db00918b363bc50f33cdb2dfe2dec22d210 (MAP-014 draft). Enrolment prerequisites are reduced to consent, immutable version, and measured resources; restore-before-approval is relabelled as proposed design per the MAP-023/MAP-026 reconciliation. Identity/key mechanism, offline-host withdrawal, recovery-custodian separation, OS/runtime, and cloud scope remain unresolved.
References: MAP-014, MAP-023, MAP-026

### controller: blocked
Controller resilience intent exists only in docs/CONCEPT.md (existing workloads should keep running during controller outages subject to dependencies; this must be tested) and docs/map/specs/backup-recovery.md at revision ccf0957af0d80fe4608fc08b06b02408b485b1ca (MAP-004 draft, Section 3 rule 7). No controller architecture, fencing, state-handling, or outage test procedure is defined in any supplied draft. MAP-008 is blocked on the coordination board (coordination-only status; document not supplied) with bounded draft corrections exhausted and modality contradictions unresolved between baseline intent and task-imposed proposals. Controller outage behaviour is an exact unresolved owner decision and technical gap; no drafting task can resolve it from supplied text.
References: baseline only; no completed task evidence

### scheduling: draft-complete
Time semantics for operating periods, assignment expiry, backups, and movement windows are defined in docs/map/specs/scheduling.md at revision 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 (MAP-007 draft): UTC storage intent unresolved, explicit timezones required for future-dated local times, DST ambiguity policy open, missed-schedule policy open, clock-skew tolerance pending MAP-003 field work, movement window is permission not migration promise. Backup creation and restore verification are kept distinct. No scheduling library or default schedule is selected.
References: MAP-007

### recovery: draft-complete
Backup operation outcome labels (Requested, Running, Verified copy, Failed), retained-copy status, restore-tested as a separate record concept, roles, unresolved values (custodian access, key separation, offline hosts, retention, RTO/RPO), evidence a later restore task must supply, and proposed record concepts are defined in docs/map/specs/backup-recovery.md at revision ccf0957af0d80fe4608fc08b06b02408b485b1ca (MAP-004 draft). No restore test was performed; restore_verified is never derived from backup creation, upload success, or integrity check (confirmed by the MAP-027 audit across 13 section checks). Emergency recovery requires a prepared target and accessible recovery data; automatic failover is a later capability.
References: MAP-004, MAP-027

### operations: draft-complete
Operational coverage overlaps interfaces (MAP-006) and scheduling (MAP-007). Release lifecycle stages (proposed, reviewed, approved-for-environment, deployed, superseded, withdrawn), dependency changes, data/schema migrations, backup prerequisites, and limits of rollback are defined in docs/map/specs/release-lifecycle.md at revision 1cd788bd77c027a6808c3c4179784a77d8ca1efe (MAP-015 draft). Rollback is explicitly not a universal promise; no runtime test or universal rollback claim exists. Open decisions from docs/DECISION-GUIDE.md remain unresolved.
References: MAP-006, MAP-007, MAP-015

### costs: blocked
No cost data exists in any supplied input. MAP-013 (Define cloud scope and spending guardrails) is blocked on the coordination board (coordination-only status; native Hermes child failed; inspect local scrubbed log; document not supplied). Cloud spending limits, provider selection, budget enforcement, and capacity-exceedance behaviour are open questions in docs/DECISION-GUIDE.md, but no enforcement mechanism, limit value, or provider is specified. Cloud costs and account permissions need controls (docs/CONCEPT.md) but remain unverified. This is an exact unavailable upstream fact and owner decision; no cost task can be drafted from supplied text.
References: baseline only; no completed task evidence

### build-and-acceptance: gap
No acceptance matrix, ordered build steps, component/data/interface map, source pins, or frozen map revision exists in any supplied input. The completion gate is not met: upstream identities, versions, and licences are unverified; interfaces, roles, data, hosting, recovery, and rollout decisions are not fully consistent; no component evidence exists; and build-blocking unknowns remain (controller outage behaviour, cloud spending limits, restore evidence). This drafting gap can be addressed from supplied text by proposing a baseline acceptance matrix structure and source-pin inventory without inventing verification.
References: baseline only; no completed task evidence

## Proposed follow-ups

### gap-key-build-and-acceptance-001: Propose baseline acceptance matrix structure and source-pin inventory from supplied sources
Area: build-and-acceptance
Draft a non-binding acceptance matrix outline from supplied text only: rows for each of the 13 coverage areas with status (draft-complete, gap, blocked), the blocking condition or missing decision, the source revisions supporting the row, and whether a runtime test or owner decision is required before acceptance. Include source pins for all four baseline inputs at revision 792b158838aa5214d0156690d24e21e780de542e and each unaccepted draft revision. Mark unresolved owner decisions (controller operator and funding, CEO succession and emergency recovery, volunteer-host workload policy, OS/runtime/cloud provider, cloud spending limits, RTO/RPO targets, offline-host withdrawal, data-reader consent, product licence) as acceptance preconditions, not resolved items. Do not certify build readiness, implementation, deployment, or any tested capability.
Checks:
- Every matrix row cites at least one supplied file path and revision as its evidence bound.
- A second observable check confirms no row claims a verified test, accepted requirement, or selected stack/provider/licence; all such items remain listed as unresolved preconditions.
- The structure is independently checkable against the supplied inputs without external research or runtime measurement.

## Exact blockers
- Controller operator and funding: who operates and pays for the central controller is an open question in docs/DECISION-GUIDE.md with no answer in any supplied input; owner decision required.
- CEO identity, delegation, succession, and emergency recovery: exact rules remain design decisions in docs/TRUST-AND-RECOVERY.md and docs/DECISION-GUIDE.md; succession must not silently grant access to historical secrets.
- Volunteer-host workload policy: which workloads are acceptable on volunteer hosts versus trusted infrastructure is unresolved in docs/DECISION-GUIDE.md and docs/TRUST-AND-RECOVERY.md.
- Pilot stack and provider: operating systems, deployment runtime, and cloud provider are unselected; Cloudflare is discussed only as an optional component; provider selection and feature suitability are unverified (docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md).
- Cloud spending limits: enforcement mechanism and over-capacity behaviour are open questions in docs/DECISION-GUIDE.md; MAP-013 is blocked on the coordination board (native Hermes child failed; inspect local scrubbed log).
- Recovery time and data-loss targets: acceptable RTO/RPO per application are open questions in docs/DECISION-GUIDE.md; required before a restore task can judge copy acceptability.
- Hardware-owner offline withdrawal: withdrawal procedure when the machine is already offline is an open question in docs/DECISION-GUIDE.md; revocation mechanics for offline hosts are not specified.
- Data-reader consent: who may read each type of corporation data and how consent is documented is an open question in docs/DECISION-GUIDE.md.
- Product licensing and distribution model: no reuse licence has been selected (README.md, docs/DECISION-GUIDE.md).
- Upstream technical verification: no upstream identity, version, licence, dependency, or cost is verified in any supplied input; candidate names (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures) are historical planning context only.
- Restore evidence: no backup or restore test has been performed or claimed; MAP-004 Section 8 states no restore test was performed; restore_verified remains unverified across all drafts (MAP-027 audit).
- Controller outage behaviour: no controller architecture, fencing, state-handling, or outage test procedure exists in supplied text; MAP-008 is blocked on the coordination board with modality contradictions unresolved between baseline intent and task-imposed proposals.
- No accepted field registry or cross-schema data model: mapping between MAP-003, MAP-005, and related drafts remains a drafting proposal, not accepted evidence; the related unification gap is tracked by blocked MAP-020 on the coordination board only (document not supplied).
