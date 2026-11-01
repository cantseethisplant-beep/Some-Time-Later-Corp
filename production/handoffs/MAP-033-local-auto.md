# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/27

Automated critic only; independent review pending.

# Coordinator format-recovery handoff

Task: MAP-033; claim commit: 5c762a6795eab82de9cc9a013ea56420b83b1551

Native content was recovered without another generation request. Expanded only uniquely matching abbreviated source pins to their supplied full immutable SHAs; Original wire response has complete file/handoff sections. Critic JSON-wrapper rejection was caused by coordinator serialization, now fixed; substantive matrix and decision register retained with no performed checks or acceptance

Sources:
- AGENTS.md @ 5c762a6795eab82de9cc9a013ea56420b83b1551
- AI-CONTEXT.md @ 5c762a6795eab82de9cc9a013ea56420b83b1551
- CONTRIBUTING.md @ 5c762a6795eab82de9cc9a013ea56420b83b1551
- docs/PRODUCTION.md @ 5c762a6795eab82de9cc9a013ea56420b83b1551
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
  "task_id": "MAP-033",
  "decision": "revise",
  "summary": "The draft covers all 13 areas with AM- check IDs, an 18-row immutable source inventory, MAP-015 release/rollback stages and Verification Checklist treated strictly as unaccepted candidate context, explicit backup-creation versus restore-exercise separation, and an OD-01 to OD-14 decision register with no check marked passed. It is, however, packaged as a JSON wrapper (task_id, status, files[], handoff_markdown) instead of the required plain-text delivery of exactly one BEGIN FILE section and one BEGIN HANDOFF section with no outer code fences or JSON wrapper, and the handoff itself claims that structure was delivered when it is not. Reformat only; the substantive content is consistent with the task contract.",
  "findings": [
    "Section/output packaging (whole draft): The draft is delivered as a JSON object (task_id, status, files[], handoff_markdown) rather than the task-contract output format, which requires exactly one plain-text BEGIN FILE: docs/map/specs/loop-map-033-assembly.md section containing the complete Markdown with a final newline, then END FILE: docs/map/specs/loop-map-033-assembly.md, then exactly one BEGIN HANDOFF section containing the handoff Markdown, then END HANDOFF, with no outer code fences or JSON wrapper. The handoff text contradicts this by stating this response returns exactly one complete BEGIN FILE / END FILE section when no such markers exist. Correction: remove the JSON envelope, task_id/status/files/handoff_markdown keys, and any code fences; emit exactly one BEGIN FILE/END FILE block with the full Markdown and exactly one BEGIN HANDOFF/END HANDOFF block with the handoff text, preserving all content.",
    "Section 3 (Acceptance and evidence matrix) length: Section 3 restates full source inventories (eight node-lifecycle states, nine operation states, MAP-015 Verification Checklist items, MAP-004 outcome labels) instead of citing the pinned revision and section, inflating the Markdown beyond the 1200-1800 word aim while the eight required AM- check fields are already present. Correction: condense Section 3 by replacing restated source content with precise citations to the pinned source revision and section, keeping all 13 areas, every AM- check's required fields, the MAP-015 unaccepted-candidate context, the backup/restore distinction, and OD-01 to OD-14 intact."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-033",
  "reviewer": "Codex coordinator — explicit user-requested assembly recovery",
  "at": "2026-11-01T16:19:36.154971+00:00",
  "native_critic_decision": "revise",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Expanded only uniquely matching abbreviated source pins to their supplied full immutable SHAs",
    "Original wire response has complete file/handoff sections. Critic JSON-wrapper rejection was caused by coordinator serialization, now fixed; substantive matrix and decision register retained with no performed checks or acceptance"
  ],
  "checks": [
    "Original raw response identity/hash and complete file envelope verified",
    "Latest native draft compared with prior critic findings",
    "Supplied source pins preserved/expanded only on unique matches",
    "No regeneration, task-budget reset, acceptance, merge, deployment or completed-test claim"
  ],
  "corrected_payload_sha256": "6052cdb78f2707319630c22dabefa191c53435d52a955028e4b22aec8301961a"
}
