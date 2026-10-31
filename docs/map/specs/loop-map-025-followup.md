# REQ-16 Rollout Row Reconciliation — MAP-025

**Task:** MAP-025 — Resolve the unsourced REQ-16 rollout row in the unified requirements table
**Claim worker:** hermes-laptop-map-025-auto-20261030
**Claim commit:** e88697f0b84ae24c2815b29f16be8033f9de5271
**Loop:** follow-up, cycle 3, area requirements, key gap-key-requirements-001 (loop policy 1)
**Output path:** docs/map/specs/loop-map-025-followup.md
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md)
**Reference draft examined:** docs/map/specs/loop-map-017-followup.md @ 552d40b359af110eb85e67f58b774de80f2b5cf8 — MAP-017 follow-up draft; unaccepted review material, not accepted requirements or technical evidence
**Status:** unaccepted proposal for review only. Not accepted requirements, not technical evidence, no app implemented or tested.

## 1. Evidence status and classification rules

All four baseline inputs — README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md and docs/TRUST-AND-RECOVERY.md — are supplied at revision 792b158838aa5214d0156690d24e21e780de542e. Evidence type: user-intent baseline; no upstream technical verification.

Requirement statements REQ-01 through REQ-17 are taken from docs/map/specs/requirements.md at revision c6cc2de20805455eb55c0343394d01225ff41ffd (MAP-001 draft), which is explicitly "UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence." Its required/proposed/optional labels are preserved here as consolidation status labels only; they do not make anything accepted.

Status taxonomy (carried from the MAP-017 draft, not new baseline facts):

- **required** — consolidation gate label carried from the MAP-001 draft; not a baseline "must" unless the Modality column says so.
- **proposed** — baseline expresses a suggestion, or the draft marks it proposed/optional and it remains unreviewed.
- **open decision** — a listed question the baseline answers nowhere; used only in Section 3 of the MAP-017 draft, never for REQ rows.

Modality rule: may/should/must are preserved exactly as the baseline phrases them and are never collapsed. Where the baseline has no explicit modal verb, Modality reads "intent" (descriptive journey or role statement) rather than inventing one. Negative constraints are preserved as written. Genuinely verified evidence: none.

## 2. REQ-16 decision: row retained, explicitly unsourced

### 2.1 Row as recorded in the MAP-017 draft (section 2)

| ID | Behaviour (summary) | Status | Modality | Source provenance | Notes |
|----|---------------------|--------|----------|-------------------|-------|
| REQ-16 | Repeatable rollout to a second corporation: configure a second isolated test corporation without copying the first corporation's private data. Desired outcome with a proposed isolation check, not a completed test. | proposed | none claimed — unsourced proposal; no baseline source section or modal verb to preserve | None claimed — unsourced proposal; MAP-001 draft records no source section | Preserved exactly as unsourced. No baseline section cited; no feasibility inferred. |

### 2.2 Decision

**REQ-16 remains in the unified requirement table, explicitly labelled as proposed-design/unsourced-only, with no baseline claim.** It is not removed pending a baseline source, because removal would suppress the visible record of an unsourced proposal and the baseline contains no section that either supports or refutes it. No modal verb, source section, or feasibility conclusion is invented for REQ-16.

### 2.3 Baseline scan performed

Every supplied baseline input at revision 792b1588... was read for any statement about rolling out to a second corporation, an isolated test corporation, or copying private data between corporations:

- **README.md** — "The idea," "What a first version might cover," and "Project boundaries" describe one corporation's hosting manager, volunteer hardware, catalogue, and roles. No second-corporation rollout, isolation check, or private-data copy provision appears.
- **docs/CONCEPT.md** — "Two build ideas" contrasts Build Idea 1 (fixed stack for one corporation) with Build Idea 2 (reusable product); "Proposed journey" steps 1–7 cover administration and recovery contacts, hardware offers, bundle selection, assignment, controlled deployment, monitoring/backups, and movement/recovery. No step describes repeatable rollout to a second corporation. The word "reusable" describes product scope, not an observable behavioural check for REQ-16, and supplies no modal verb or source section for it.
- **docs/DECISION-GUIDE.md** — Choice matrix, catalogue entry requirements, and open questions contain no second-corporation rollout statement.
- **docs/TRUST-AND-RECOVERY.md** — Proposed roles, hardware boundaries, and backup and movement contain no second-corporation rollout statement.

Result: no baseline section supports REQ-16. The MAP-001 draft itself records the row as "none claimed — unsourced proposal; no baseline source section or modal verb to preserve." That record is preserved verbatim in Section 2.1 above.

### 2.4 What was deliberately not done

- No baseline modal verb (should/must/may) was assigned to REQ-16.
- No baseline source section was cited for REQ-16.
- No feasibility or isolation-check conclusion was drawn.
- The baseline's general reusability language (Build Idea 2 as a "reusable product") was not treated as a source for REQ-16, because it is product intent, not an observable behavioural check, and it names no isolation procedure.

## 3. Distinctions preserved in this draft

- **Baseline intent:** the four user-approved concept documents at revision 792b1588..., the origin of every behaviour in the unified table. REQ-16 has no origin here.
- **Proposed design:** the status taxonomy, modality annotations, open-decision enumeration, and the REQ-16 "proposed-design/unsourced-only" label added by MAP-017 and carried forward by MAP-025; not accepted until separately reviewed.
- **Completed unaccepted reference drafts:** docs/map/specs/requirements.md (MAP-001 draft, source of REQ-01..REQ-17) and the MAP-017 draft itself are review material only. They are not accepted requirements, dependency satisfaction, or verified technical evidence.
- **Genuinely verified evidence:** none. No runtime tests, restore tests, component tests, or integration checks exist in the supplied inputs, and none are claimed here.

## 4. Section 5 modality audit — REQ-16 treated as "none claimed"

The modality audit in section 5 of the MAP-017 draft is reproduced here for REQ-16 and treated as binding for this reconciliation:

- REQ-16: no baseline modal verb exists; recorded as "none claimed" rather than inventing should.

Consequences:

- REQ-16 is **not** upgraded to "should" or "must" anywhere in this draft.
- No hard gate, isolation check, or rollout feasibility condition is imposed on the basis of REQ-16.
- Any hard gate beyond the baseline's own verbs would be labelled proposed-design, never a baseline mandate.

This audit is consistent with docs/map/specs/loop-map-017-followup.md section 5, which records REQ-16 as "none claimed" and explicitly declines to invent a modal verb.

## 5. Acceptance criteria mapping and checks performed

| Acceptance criterion | How it is met |
|---|---|
| REQ-16 row either cites a baseline section with an observable behavioural check, or is marked proposed-design/unsourced-only with no baseline modality; traceable to section 2 and section 5 | Section 2.1 retains REQ-16 with Modality "none claimed — unsourced proposal; no baseline source section or modal verb to preserve" and Source provenance "None claimed — unsourced proposal; MAP-001 draft records no source section". Traceable to section 2 (row) and section 4 (modality audit). |
| Section 5 modality audit treats REQ-16 as "none claimed" rather than upgrading to should/must, consistent with section 5 of the MAP-017 draft | Section 4 above records REQ-16 as "none claimed" and lists what was not done (no verb, no section, no feasibility conclusion). |
| Explicitly distinguish baseline intent, proposed design, completed unaccepted reference drafts and genuinely verified evidence | Section 3 above. |

Checks performed:

1. Read docs/map/specs/loop-map-017-followup.md @ 552d40b3... in full, specifically section 2 (unified requirement table, row REQ-16) and section 5 (modality audit).
2. Read all four baseline inputs @ 792b1588... (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md) and searched each for "second corporation", "rollout", "isolated", "test corporation", and private-data copying; no matches relevant to REQ-16 were found.
3. Cross-checked the REQ-16 row wording against the MAP-001 draft (docs/map/specs/requirements.md @ c6cc2de2...): both record REQ-16 as unsourced with no baseline section.
4. Confirmed the MAP-001 draft and MAP-017 draft are each labelled unaccepted review material only, so neither can supply a baseline citation for REQ-16.
5. Verified no modal verb, source section, feasibility conclusion, or removal decision is invented in this draft.

## 6. Limitations and review pending

No GitHub, terminal, network or delegation tools are available; board state and file SHAs were not independently verified. MAP-001..MAP-011 drafts and MAP-017..MAP-023 follow-up drafts are treated as unaccepted review material, not evidence. No technical verification of upstream software, licence, cost, restore, or hosting claims has been performed, and none is claimed.

This document is a planning/reconciliation draft only. Acceptance rests with the project owner or an appointed reviewer; nothing is self-accepted. Up to two document corrections may apply under task policy; acceptance and any merge remain with the project owner or appointed reviewer.

Remaining work: coordinator/owner review of this draft.

Review pending: yes — the draft is review input only; no submission, claim release or board update has been performed by this worker.

