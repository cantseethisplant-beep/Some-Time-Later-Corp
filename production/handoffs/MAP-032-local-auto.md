# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/26

Automated critic only; independent review pending.

# Coordinator format-recovery handoff

Task: MAP-032; claim commit: e26ec68b5278365ce052503f66a2019dde67510f

Native content was recovered without another generation request. Added the proposed hardware-offer backup_policy_ref crosswalk verified against supplied MAP-003 section 3 field 9 and MAP-004; policy ownership/evidence remains separate; Verified latest native generation already distinguishes proposed storage split, node-state provenance and OD-01; word-count aim is not a mandatory rejection gate

Sources:
- AGENTS.md @ e26ec68b5278365ce052503f66a2019dde67510f
- AI-CONTEXT.md @ e26ec68b5278365ce052503f66a2019dde67510f
- CONTRIBUTING.md @ e26ec68b5278365ce052503f66a2019dde67510f
- docs/PRODUCTION.md @ e26ec68b5278365ce052503f66a2019dde67510f
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
- docs/map/specs/loop-map-023-followup.md @ 810cc1f9ad0dc411977f3d37ba8b37e6e1980359
- docs/map/specs/loop-map-025-followup.md @ 57dfe172304d5fcf2f19a98f3c16ccbd57131442
- docs/map/specs/loop-map-026-followup.md @ d45c7a945523ca05447cf8f9757b171fd319b5da
- docs/map/specs/loop-map-027-followup.md @ 6b4aa91aebf4c07de0a9c239ad0b07eb0f6da2de
- production/proposals/blueprint-005.json @ 4e3dec35f8da85e6fb2668550fe592368a31fc22

Only envelope parsing and declared schema checks were performed. Independent acceptance, technical verification and build readiness are not established. Full original response and its SHA-256 are preserved locally.


## Automated screening
{
  "task_id": "MAP-032",
  "decision": "revise",
  "summary": "The MAP-032 assembly draft preserves baseline/proposed labels, consent and deployment/decryption boundaries, and backup/restore separation, with a complete pinned input inventory and per-row citations. Two issues require revision before it can be a clean review submission: the node/host glossary row over-attributes the eight lifecycle states to CONCEPT.md when they are defined only in MAP-014 section 2, and section 8 omits OD-01 (who operates and pays for the central controller) from the unresolved decisions carried forward from DECISION-GUIDE.md.",
  "findings": [
    "Section 5 glossary row 'node / host' cites 'CONCEPT.md; MAP-014 section 2' for the volunteered-node definition and the eight lifecycle states together, but CONCEPT.md does not define the offered→enrolment-pending→approved→active→disconnected→draining→revoked→retired state machine; that comes only from the MAP-014 draft section 2 (proposed schema). Correction: split the source cell so CONCEPT.md supports only the node/offer concept and MAP-014 section 2 is cited as the proposed source for the eight states, keeping status 'proposed schema'.",
    "Section 8 'Contract disagreements and unresolved choices' carries forward OD-02 through OD-14 but omits OD-01, 'Who operates and pays for the central controller?' from docs/DECISION-GUIDE.md 'Questions still open', an open baseline decision about the controller. Correction: add OD-01 to the section 8 unresolved list (and to section 11 limitations) citing DECISION-GUIDE.md 'Questions still open' so no open decision is silently dropped."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-032",
  "reviewer": "Codex coordinator — explicit user-requested assembly recovery",
  "at": "2026-11-01T16:19:24.438932+00:00",
  "native_critic_decision": "revise",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Added the proposed hardware-offer backup_policy_ref crosswalk verified against supplied MAP-003 section 3 field 9 and MAP-004; policy ownership/evidence remains separate",
    "Verified latest native generation already distinguishes proposed storage split, node-state provenance and OD-01; word-count aim is not a mandatory rejection gate"
  ],
  "checks": [
    "Original raw response identity/hash and complete file envelope verified",
    "Latest native draft compared with prior critic findings",
    "Supplied source pins preserved/expanded only on unique matches",
    "No regeneration, task-budget reset, acceptance, merge, deployment or completed-test claim"
  ],
  "corrected_payload_sha256": "4fe2f4c47a7f0001df2921f48ed19854af9db23ad2a0ac9eda19ff1ad8b18c81"
}
