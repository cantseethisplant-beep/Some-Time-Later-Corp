# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/17

Automated critic only; independent review pending.

# Coordinator format-recovery handoff

Task: MAP-022; claim commit: 2ab588a985fa29804f2a3e7af73c653a566c4f19

Native content was recovered without another generation request. Preserved original response locally; moved pinned-board-only references to labelled assessment text, explicitly not source evidence; output schema unchanged; Rendered normalised audit from its validated fields; Codex coordinator verified the native critic finding against pinned MAP-014 section 5, MAP-004 section 5 and TRUST-AND-RECOVERY; added one independently executable reconciliation task and withdrew the unsupported no-follow-up assertion. No further inference or acceptance.

Sources:
- AGENTS.md @ 2ab588a985fa29804f2a3e7af73c653a566c4f19
- AI-CONTEXT.md @ 2ab588a985fa29804f2a3e7af73c653a566c4f19
- CONTRIBUTING.md @ 2ab588a985fa29804f2a3e7af73c653a566c4f19
- docs/PRODUCTION.md @ 2ab588a985fa29804f2a3e7af73c653a566c4f19
- README.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/CONCEPT.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/DECISION-GUIDE.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/map/specs/requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd
- docs/map/specs/permissions.md @ 3585afed129ad2694660fcee8cfd982092551117
- docs/map/specs/hosting-assignment.md @ 0e60848ccbfa295169422eab063f1b81023b390e
- docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca
- docs/map/specs/catalogue-entry.md @ 96464d45c5c79db31a82bcb9cf13a1b1b65fb141
- docs/map/specs/operations.md @ 111a5832102570811dd0af21fffd16a70413febc
- docs/map/specs/scheduling.md @ 9f330ee125a04bdd6f5df1338b38c93ff2fe0162
- docs/map/specs/evidence-record.md @ 119bb89f6decab9c887e0e99bde38e7d6b1a6744
- docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210
- docs/map/specs/release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe
- docs/map/specs/loop-map-017-followup.md @ 552d40b359af110eb85e67f58b774de80f2b5cf8
- docs/map/specs/loop-map-019-followup.md @ 41c48febc50f58304a164ebc4abe174e891193ee

Only envelope parsing and declared schema checks were performed. Independent acceptance, technical verification and build readiness are not established. Full original response and its SHA-256 are preserved locally.


## Automated screening
{
  "task_id": "MAP-022",
  "decision": "revise",
  "summary": "The MAP-022 draft covers all 13 areas with source-referenced assessments and preserves baseline/proposed modality, but its empty tasks array and the matching blocker ('no non-duplicative follow-up is independently executable') are unsupported. A concrete, independently executable contradiction exists between two MAP-022 supplied inputs: MAP-014 section 5 makes a tested restore exercise a required enrolment gate (offered to approved) citing TRUST-AND-RECOVERY, while MAP-004 sections 5 and 8 defer restore verification to a later task and claim no completed restore test, and the baseline ties restore-exercise to recoverability proof rather than node enrolment or approval. No owner decision is needed; only MAP-014, MAP-004 and TRUST-AND-RECOVERY are required. The draft must add a small reconciliation task with observable checks, or explicitly justify excluding it.",
  "findings": [
    "tasks array empty and blocker overstated: MAP-014 section 5 (rev 39981db00918b363bc50f33cdb2dfe2dec22d210) lists 'Backup/restore evidence: A tested restore exercise must exist for the assigned application bundle' as required trust evidence before the offered-to-approved node transition, citing TRUST-AND-RECOVERY.md, whereas MAP-004 sections 5 and 8 (rev ccf0957af0d80fe4608fc08b06b02408b485b1ca) position restore verification as evidence a later restore task must supply and explicitly claim no completed restore test; the baseline (TRUST-AND-RECOVERY, Backup and movement) ties the restore-exercise requirement to recoverability proof, not to node enrolment or approval. This is a baseline-versus-proposed modality defect and an input-versus-input contradiction fixable now from MAP-022 sources alone with no owner decision. Correction: add a reconciliation task with a stable key (area node-security or recovery) that re-labels MAP-014 section 5's restore-before-approval rule as proposed-design or removes the baseline citation for that gate; observable checks: (1) MAP-014 section 5 either drops the TRUST-AND-RECOVERY citation for the enrolment-precondition reading or marks the rule proposed-design, and (2) MAP-014 does not claim a completed restore test, deferring evidence to later integration. This is not covered by an existing loop key (MAP-014 loop_key is null), so it is not duplicative. Withdraw or revise the 'no executable follow-up' blocker accordingly."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-022",
  "reviewer": "Codex coordinator — user-requested repair",
  "at": "2026-10-31T08:25:57.701803+00:00",
  "native_critic_decision": "revise",
  "native_critic_draft_sha256": "7625fbf520d7a482fb1a54bed8342cb93a1783806bcc1b2d43389118c426f7eb",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Native critic identified the unsupported empty-task assertion. Coordinator verified MAP-014 39981db00918b363bc50f33cdb2dfe2dec22d210 section 5 against MAP-004 ccf0957af0d80fe4608fc08b06b02408b485b1ca section 5 and the pinned TRUST-AND-RECOVERY baseline.",
    "Added node-approval-restore-proof-boundary as a bounded drafting/reconciliation task; no new research, owner decision or runtime evidence is required to draft the note. It will not modify original drafts or invent a completed test.",
    "Changed node-security/recovery coverage to gap, recalculated summary counts and removed the false no-executable-follow-up blocker. Other evidence and owner-decision blockers remain.",
    "Board-only references are labelled coordination status in existing assessment text; no extra output fields or promotion of blocked drafts to source evidence."
  ],
  "checks": [
    "All 13 coverage areas and declared output schema validated",
    "All source_tasks identify supplied immutable completed drafts",
    "New task is independent supplied-text work with observable checks and no implementation",
    "Native critic findings and pre-correction packet preserved",
    "No counter reset, native recheck, project acceptance or merge"
  ],
  "corrected_payload_sha256": "85756c1e9e54f9c9a680e6b2aa84294392f887f35d24c69395357ef58baedb53"
}
