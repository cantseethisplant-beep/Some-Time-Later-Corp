# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/15

Automated critic only; independent review pending.

MAP-017 follow-up draft — coordinator handoff record

Task: MAP-017 — Consolidate and clarify requirement modalities and open decisions
Claim worker: hermes-laptop-map-017-auto-20261030
Claim commit (not a token): bfd59c7f841e6db08a8003aee31f6edee5ec1b49
Loop kind: follow-up; loop cycle: 1; loop area: requirements; loop key: gap-key-requirements-001; loop policy: 1
Output path produced: docs/map/specs/loop-map-017-followup.md (complete file section included above)

Diagnosed issue and exact correction:
1. REQ-16 Modality assigned "should — desired outcome..." although REQ-16 is explicitly unsourced (no baseline section and no baseline modal verb). This invented a modality for an unsourced proposal and contradicted the no-unsupported-inferences rule plus the scope rule to preserve REQ-16 as an unsourced proposal. Exact correction: Section 2, row REQ-16, Modality cell changed to "none claimed — unsourced proposal; no baseline source section or modal verb to preserve". The unsupported "should" was dropped; provenance remains "None claimed — unsourced proposal; MAP-001 draft records no source section".

Previously applied corrections (re-verified and preserved in this version): REQ-01 Modality "intent" with no baseline verb upgraded; REQ-02 recording/availability not escalated to must; REQ-04 baseline "should" preserved with hard gate labelled proposed-design; REQ-08 Status proposed with could/may, retention/exact times tracked as OD-14; REQ-17 split provenance (baseline "may withdraw" vs MAP-001-draft recorded/excluded wording); REQ-06 "may" with no inferred should for health exposure.

Exact sources used:
- revision 792b158838aa5214d0156690d24e21e780de542e — README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md (user-intent baseline; no upstream technical verification)
- revision c6cc2de20805455eb55c0343394d01225ff41ffd — docs/map/specs/requirements.md (MAP-001 draft; source of REQ-01..REQ-17 text; UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY)
- MAP-002, MAP-003, MAP-004, MAP-005, MAP-006, MAP-007 and MAP-011 drafts inventoried as supplied inputs; not cited in this draft's tables.

Checks actually performed:
- Inventory of all nine supplied inputs at their pinned revisions.
- REQ-01..REQ-17 extracted from the MAP-001 draft and cross-checked against baseline sections.
- Baseline revision confirmed as 792b1588... for the four concept inputs.
- Per-row modality audit against baseline verbs (may/should/must/intent; no collapse).
- Open decisions enumerated from DECISION-GUIDE.md "Questions still open" and TRUST-AND-RECOVERY.md sections (Proposed roles, Hardware boundaries, Backup and movement), each pinned to a source section and marked unresolved.
- REQ-16 confirmed unsourced (no baseline section, no modal verb); REQ-17 baseline reference confirmed with MAP-001-draft wording attributed separately.
- Required fields checked against every example/row; unresolved policy not mandated anywhere in the document.
- Acceptance criteria mapped in draft Section 6.

Limitations: No GitHub, terminal, network or delegation tools available; board state and file SHAs not independently verified. MAP-001..MAP-011 drafts treated as unaccepted review material, not evidence. No runtime/restore/component/integration tests performed or claimed. No owner decision resolved; no stack, provider, cost, licence, or implementation chosen. This draft is review input only.

Remaining work: coordinator/owner review of the draft; up to two document corrections may apply under task policy; acceptance decision and any merge remain with the project owner/appointed reviewer.

Review pending: yes — draft is review input only; no submission, claim release or board update has been performed by this worker.


## Automated screening
{
  "task_id": "MAP-017",
  "decision": "submit_draft",
  "summary": "The draft satisfies all MAP-017 acceptance criteria: a unified table covers REQ-01..REQ-17 with Status (required/proposed), preserved may/should/must/intent modality, and source provenance per row (REQ-16 explicitly unsourced with no baseline section; REQ-17 split baseline vs MAP-001-draft wording). Section 3 enumerates OD-01..OD-14 as unresolved with pinned source sections and rationales, resolving no owner choice. Section 4 separates baseline intent, proposed design, unaccepted reference drafts, and verified evidence (none claimed). No unsupported inferences, invented evidence, backup/restore conflation, or mandatory unresolved policy in examples are present.",
  "findings": []
}
