# Blueprint coverage audit — unaccepted draft

This human-readable view is rendered deterministically from the native Hermes JSON audit. It adds no facts or verification. Independent review remains pending.

MAP-024 audit of the usable-blueprint completion gate across all 13 areas, using only the supplied inputs at their pinned revisions. Eight areas have supplied unaccepted drafts (requirements via MAP-001/MAP-003/MAP-017; roles via MAP-002; catalogue via MAP-005; upstream-evidence via MAP-011/MAP-019; node-security via MAP-014/MAP-023; scheduling via MAP-007; recovery via MAP-004/MAP-015; operations via MAP-006). Five areas (data-model, interfaces, controller, costs, build-and-acceptance) have no supplied input; related tasks appear on the coordination board as blocked but their drafts are not supplied and are recorded as status only, not reassessed. No supplied text establishes an accepted requirement, a tested component, a restore, or build-readiness. Three independent reconciliation tasks are proposed from supplied text only; every other open item is recorded as an owner or evidence blocker.

## Coverage

### requirements: draft-complete
MAP-001 draft (docs/map/specs/requirements.md, rev c6cc2de2...) supplies REQ-01..REQ-17 with summary behaviour, status (required/proposed), modality, source path/section and an observable behavioural check per row, plus a glossary, proposed safeguards, and open decisions. MAP-003 draft (docs/map/specs/hosting-assignment.md, rev 0e60848c...) adds proposed hardware-offer and assignment field shapes (offer fields 1-10, assignment fields 1-13, required subsets, case states valid/invalid/withdrawn/offline) marked as proposed design, not baseline. MAP-017 follow-up (docs/map/specs/loop-map-017-followup.md, rev 552d40b3...) consolidates REQ-01..REQ-17 with a preserved-modality audit and enumerates open decisions OD-01..OD-14 pinned to docs/DECISION-GUIDE.md and docs/TRUST-AND-RECOVERY.md. Limits: all three are unaccepted review material, not accepted requirements; REQ-16 has no baseline source section or modal verb and is recorded as unsourced (task gap-key-requirements-001); retention and exact assignment times (OD-14) are undecided; no runtime evidence exists.
References: MAP-001, MAP-003, MAP-017

### roles: draft-complete
MAP-002 draft (docs/map/specs/permissions.md, rev 3585afed...) supplies five roles (CEO, appointed manager, hardware owner, member, recovery custodian), a seven-action role/action matrix with consent conditions and boundaries, separation of deployment authority and decrypt permission, and explicit unresolved decisions for CEO succession, emergency access, and delegation (section 6). Limits: unaccepted draft only; succession/emergency/delegation rules remain owner design decisions; MAP-018 appears on the coordination board as blocked with loop_key gap-key-roles-001 but its draft is not supplied and is not reassessed here.
References: MAP-002

### catalogue: draft-complete
MAP-005 draft (docs/map/specs/catalogue-entry.md, rev 96464d45...) supplies four entry states (candidate, documentation-reviewed, component-tested, supported-for-specific-environment) with minimum evidence, required vs optional fields across identity/provenance, dependencies, permissions/trust, resources, deployment/update/rollback/movement/controller-outage, and backup/restore evidence kept as distinct items, plus evidence conditions, invalidation triggers, and a synthetic labelled example where restore_verified is synthetic and never derived from backup upload. Limits: schema proposal only, unaccepted; no upstream candidate researched (Wanderer et al. are historical context only); no measured resources, licence, or stack selected.
References: MAP-005

### upstream-evidence: draft-complete
MAP-011 draft (docs/map/specs/evidence-record.md, rev 119bb89f...) supplies five evidence categories kept separate (user intent, proposed design, documentation-reviewed, component-tested, integration-tested), a common provenance schema with invalidation triggers and affected_records, targeted reopening rules, and synthetic templates all marked not performed. MAP-019 follow-up (docs/map/specs/loop-map-019-followup.md, rev 41c48feb...) adds a documentation-reviewed template with populated synthetic example, per-category invalidation trigger patterns, and an intent-to-component-tested progression path. Limits: genuinely verified evidence is none; no component, integration, restore, or cost test exists in the supplied inputs; templates are not evidence.
References: MAP-011, MAP-019

### data-model: gap
gap. No supplied input defines or unifies the data model across catalogue entries, offers, and assignments. MAP-020 appears on the coordination board as blocked with loop_key gap-key-data-model-001, and the board summary notes two correctable defects (a duplicated expiry item and a misattributed Retention row), but the MAP-020 draft is not among the supplied inputs; board findings are recorded status only and are not independent reassessment or evidence that the defects were fixed.
References: baseline only; no completed task evidence

### interfaces: gap
gap. No supplied input defines the minimal interface contract. MAP-021 appears on the coordination board as blocked with loop_key gap-key-interfaces-001, and the board summary notes modality/citation issues (IA-02 should-modality vs baseline; IA-01 treating proposed validity conditions as baseline gates), but the MAP-021 draft is not supplied and is not reassessed.
References: baseline only; no completed task evidence

### node-security: draft-complete
MAP-014 draft (docs/map/specs/node-lifecycle.md, rev 39981db0...) supplies eight lifecycle states (offered, enrolment-pending, approved, active, disconnected, draining, revoked, retired), consent boundaries, and an explicit separation of management-access removal from verified workload/data cleanup; trust evidence for offered->approved lists consent, immutable version, measured resources, and backup/restore evidence. MAP-023 follow-up (docs/map/specs/loop-map-023-followup.md, rev 810cc1f9...) identifies that MAP-014 section 5 presents restore-before-approval as baseline-derived trust evidence although the baseline and MAP-004 (sections 5 and 8) locate restore proof with a later task, allow 'not performed', and claim no restore test; MAP-023 proposes replacement wording (unaccepted). Limits: unaccepted drafts; identity/key mechanism and offline withdrawal unresolved (task node-approval-restore-proof-boundary).
References: MAP-014, MAP-023

### controller: gap
gap. No supplied input covers controller outage behaviour as a standalone specification. MAP-008 appears on the coordination board as blocked with modality contradictions (hard requirement vs baseline intent vs task-imposed proposed rows; an unlabeled recording mandate), but the MAP-008 draft is not supplied and is not reassessed. Baseline intent only, from docs/CONCEPT.md: workloads should keep running during controller outages subject to dependencies, and this must be tested.
References: baseline only; no completed task evidence

### scheduling: draft-complete
MAP-007 draft (docs/map/specs/scheduling.md, rev 9f330ee1...) supplies time semantics: UTC storage as an unresolved proposal (not a mandate), explicit timezones with IANA zones, DST spring-forward/fall-back ambiguity, missed schedules, clock-skew tolerance for fencing, movement window as a time-based permission not a migration promise, and backup creation kept distinct from restore verification, with boundary examples that select no resolution. Limits: all storage convention, display rule, DST resolution, missed-schedule policy, skew tolerance, schedule ownership, and expiry-access decisions are unresolved policy listed in section 7; no defaults are invented.
References: MAP-007

### recovery: draft-complete
MAP-004 draft (docs/map/specs/backup-recovery.md, rev ccf0957a...) supplies operation outcome labels (Requested, Running, Verified copy, Failed), retained-copy status and restore-tested as separate concepts, behaviour rules (same procedure for manual and scheduled backups, no live standby, no vendor or encryption choice, planned-move steps, emergency recovery on a prepared target, controller resilience), roles, unresolved values (custodian access, key separation, offline hosts, retention, data-loss/recovery targets), evidence a later restore task must supply, proposed record concepts, and synthetic examples. MAP-015 draft (docs/map/specs/release-lifecycle.md, rev 1cd788bd...) adds release lifecycle stages, dependency changes, data/schema migrations, backup prerequisites before release transitions, and rollback limits, marked unaccepted. Limits: no backup or restore test is performed or claimed anywhere in the supplied inputs; recovery acceptability cannot be judged.
References: MAP-004, MAP-015

### operations: draft-complete
MAP-006 draft (docs/map/specs/operations.md, rev 111a5832...) supplies nine operation states (requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required) with transition constraints, minimum record fields, truthful progress and timeout/unknown-outcome handling, five error classes, retry/idempotency rules with no success inferred from launch, synthetic cases, and an explicit boundary not redefining the MAP-004 backup contract. Limits: unaccepted draft; default timeouts, retry budgets, idempotency key ownership, recovery-required SLA, and application-specific acceptance conditions are unresolved policy in section 7.
References: MAP-006

### costs: gap
gap. No supplied input defines cloud spending guardrails or a cost model. MAP-013 appears on the coordination board as blocked; its draft is not supplied. Baseline open question OD-05 (spending-limit enforcement and over-capacity behaviour) is unresolved; no provider, licence, or cost is selected or verified.
References: baseline only; no completed task evidence

### build-and-acceptance: gap
gap. No supplied input is a build-and-acceptance record. MAP-012 appears on the coordination board as blocked; its draft is not supplied. No acceptance checks, component evidence, frozen map revision, or build-ready status exist in the supplied inputs; the completion gate conditions are not met, and nothing here certifies acceptance, merge, implementation, deployment, or build-readiness.
References: baseline only; no completed task evidence

## Proposed follow-ups

### gap-key-requirements-001: Resolve the unsourced REQ-16 rollout row in the unified requirements table
Area: requirements
In docs/map/specs/loop-map-017-followup.md section 2 row REQ-16 ('Repeatable rollout to a second corporation') the draft records 'none claimed — unsourced proposal; no baseline source section or modal verb to preserve'. Decide from supplied text only whether REQ-16 remains in the table explicitly labelled as proposed-design/unsourced with no baseline claim, or is removed pending a baseline source. Do not invent a modal verb, source section, or feasibility conclusion. This is a drafting/reconciliation change to the unaccepted MAP-017 draft only.
Checks:
- REQ-16 row either cites a baseline section with an observable behavioural check, or is marked proposed-design/unsourced-only with no baseline modality; either outcome is traceable to docs/map/specs/loop-map-017-followup.md section 2 and section 5.
- Section 5 modality audit treats REQ-16 as 'none claimed' rather than upgrading it to should/must, consistent with docs/map/specs/loop-map-017-followup.md section 5.

### node-approval-restore-proof-boundary: Reconcile the node enrolment gate with restore-proof evidence (MAP-014 section 5 vs MAP-004 sections 5 and 8)
Area: node-security
In docs/map/specs/node-lifecycle.md section 5, 'A tested restore exercise must exist' is listed among trust evidence required before offered->approved, presented as baseline-derived. The baseline (docs/TRUST-AND-RECOVERY.md) requires a restore exercise to prove recoverability but does not make it an enrolment gate; MAP-004 sections 5 and 8 place restore evidence with a later task, include 'not performed', and claim no restore test. Adopt the MAP-023 proposed replacement wording (docs/map/specs/loop-map-023-followup.md section 4): enrolment requires hardware owner consent, application reviewed immutable version, and measured resources only; demonstrated recoverability is separated as assignment-readiness/owner-policy and is explicitly proposed, not baseline-mandated. No implementation, no policy choice, and no test is introduced.
Checks:
- Replacement section 5 lists enrolment prerequisites (consent, immutable version, measured resources) and excludes restore-before-approval from baseline claims; any restore-gating policy is labelled proposed design, with citations to docs/TRUST-AND-RECOVERY.md and docs/map/specs/backup-recovery.md sections 5 and 8.
- Restore-exercise result categories (attempted, succeeded, failed, not performed) and the statement that no restore test was performed are retained via the MAP-004 cross-reference; backup integrity and restore verification remain distinct.

### gap-key-backup-restore-distinction: Audit supplied drafts for any wording that derives restore verification from backup creation
Area: recovery
Audit the supplied drafts (MAP-004 sections 2/5/6, MAP-005 sections 4.6/7/9, MAP-011 sections 3/7, MAP-019 sections 3/5/7, MAP-023 sections 5/6) for any wording that derives restore verification from backup creation or upload success. Confirm each draft keeps backup creation and restore verification as distinct evidence items with restore_verified never derived from a backup record. Draft a minimal correction only where residual phrasing conflates the two; if none is found, record the audit outcome as 'confirmed: no change required' with the drafts and sections checked cited as provenance.
Checks:
- A cited list of the checked drafts and sections showing backup fields and restore fields are separate in each (for example MAP-005 section 9 check and MAP-023 section 6 distinction).
- Either a concrete correction draft for any conflation found, traceable to the specific draft and section, or a recorded finding that no supplied draft derives restore_verified from backup upload, with the list of checked sections as provenance.

## Exact blockers
- Owner decisions required (baseline open questions, answered by no supplied draft): who operates and pays for the central controller; CEO identity, delegation, succession and emergency recovery; which workloads are acceptable on volunteer hosts versus trusted infrastructure; pilot OS, deployment runtime and cloud provider; cloud spending-limit enforcement and over-capacity behaviour; acceptable recovery time and data-loss targets per application; hardware-owner withdrawal including when the machine is offline; who may read each corporation data type and how consent is documented; product licensing and distribution model. Pinned to docs/DECISION-GUIDE.md 'Questions still open' and docs/TRUST-AND-RECOVERY.md at revision 792b158838aa5214d0156690d24e21e780de542e.
- No upstream identity, version, licence, dependency, or cost is verified for any candidate application (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures, CorpTools are historical planning context only, per docs/DECISION-GUIDE.md and docs/CONCEPT.md).
- No restore test exists in the supplied inputs: MAP-004, MAP-011 and MAP-019 all state no restore was performed and restore_exercise/restore_verified remain 'not performed'; recovery acceptability cannot be judged.
- No measured resources, measured data-loss window, or selected deployment target/runtime exist; estimates are not treated as measurements (docs/DECISION-GUIDE.md catalogue entry requirements).
- No supplied draft covers data-model (MAP-020), interfaces (MAP-021), controller (MAP-008), or costs (MAP-013); those tasks appear on the coordination board as blocked and their drafts are unavailable, so no drafting can proceed from supplied text.
- Nothing in this audit certifies acceptance, merge, implementation, deployment, or build-readiness; the completion gate is not met and no frozen map revision exists.
