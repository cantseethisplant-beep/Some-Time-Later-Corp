# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/28

Automated critic only; independent review pending.

# Coordinator format-recovery handoff

Task: MAP-034; claim commit: f66ae809ee33d9c3efc06c776780ad42a7441d35

Native content was recovered without another generation request. Verified latest native title, REQ-03 action, REQ-04 proposed gate and evidence labels; marked missing-part statements as historical input-snapshot context and linked newly published parts without pretending the native task consumed them

Sources:
- AGENTS.md @ f66ae809ee33d9c3efc06c776780ad42a7441d35
- AI-CONTEXT.md @ f66ae809ee33d9c3efc06c776780ad42a7441d35
- CONTRIBUTING.md @ f66ae809ee33d9c3efc06c776780ad42a7441d35
- docs/PRODUCTION.md @ f66ae809ee33d9c3efc06c776780ad42a7441d35
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
  "task_id": "MAP-034",
  "decision": "revise",
  "summary": "The draft content covers the required blueprint areas (navigation index, bounded MVP, numbered build order, requirement-to-check matrix, component/data/interface map, trust boundaries, release/rollback and backup/restore path, source inventory, acceptance matrix, open decisions, build prerequisites, decision list, limitations and builder instructions) and preserves unaccepted-draft labels with no acceptance or stack certification. However, it fails the mandatory output format: it is packaged as a JSON wrapper (task_id, status, files[], notes[], handoff_markdown) instead of exactly one BEGIN FILE section and one BEGIN HANDOFF section with no outer code fences or JSON wrapper — the same non-conformance previously flagged for MAP-033. Its source inventory also mixes a full baseline revision with abbreviated 7-char draft revisions, weakening the 'exact immutable source references' requirement. Both issues are fixable from the supplied inputs.",
  "findings": [
    "Output format defect: the draft is delivered as a JSON object (task_id, status, files[], notes[], handoff_markdown) instead of the required plain-text delivery of exactly one BEGIN FILE: docs/map/specs/loop-map-034-candidate.md section containing the complete markdown with a final newline, followed by one BEGIN HANDOFF section on its own line carrying task/claim COMMIT f66ae809ee33d9c3efc06c776780ad42a7441d35, exact sources, checks performed, limitations, remaining work and review pending, then END HANDOFF, with no outer code fences or JSON wrapper (PINNED SOURCES AND RULES; same non-conformance previously flagged for MAP-033). Correction: re-emit under BEGIN FILE / END FILE and BEGIN HANDOFF / END HANDOFF only, dropping the outer JSON object, files[] wrapper and code fences.",
    "Source reference exactness: §2 Immutable source inventory states the baseline at full revision 792b158838aa5214d0156690d24e21e780de542e but lists completed drafts only with abbreviated 7-char revisions (e.g., MAP-001 @ c6cc2de2) instead of the full pinned revisions from the task contract inputs, weakening the required 'exact immutable source references' and creating an inconsistent baseline-full vs draft-short style. Correction: restate every supplied input with its full 40-char git revision (e.g., docs/map/specs/requirements.md @ c6cc2de20805455eb55c0343394d01225ff41ffd) so all source references are exact and immutable."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-034",
  "reviewer": "Codex coordinator — explicit user-requested assembly recovery",
  "at": "2026-11-01T16:19:49.330514+00:00",
  "native_critic_decision": "revise",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Verified latest native title, REQ-03 action, REQ-04 proposed gate and evidence labels; marked missing-part statements as historical input-snapshot context and linked newly published parts without pretending the native task consumed them"
  ],
  "checks": [
    "Original raw response identity/hash and complete file envelope verified",
    "Latest native draft compared with prior critic findings",
    "Supplied source pins preserved/expanded only on unique matches",
    "No regeneration, task-budget reset, acceptance, merge, deployment or completed-test claim"
  ],
  "corrected_payload_sha256": "938a5ca10a1115d9390b67d448e92b9036128c41394235a72d6ba0128575684e"
}
