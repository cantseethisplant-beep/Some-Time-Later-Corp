# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/24

Automated critic only; independent review pending.

# Coordinator format-recovery handoff

Task: MAP-030; claim commit: 3b8bb2cb28e9463beb3582419b76749cc53f3127

Native content was recovered without another generation request. Preserved native JSON exactly; rendered companion Markdown from its validated fields; Codex coordinator verified supplied MAP-015 @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe and added its release/rollback/checklist context to operations and build-and-acceptance coverage. All area statuses unchanged; no performed tests, accepted criteria or capability inferred.

Sources:
- AGENTS.md @ 3b8bb2cb28e9463beb3582419b76749cc53f3127
- AI-CONTEXT.md @ 3b8bb2cb28e9463beb3582419b76749cc53f3127
- CONTRIBUTING.md @ 3b8bb2cb28e9463beb3582419b76749cc53f3127
- docs/PRODUCTION.md @ 3b8bb2cb28e9463beb3582419b76749cc53f3127
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

Only envelope parsing and declared schema checks were performed. Independent acceptance, technical verification and build readiness are not established. Full original response and its SHA-256 are preserved locally.


## Automated screening
{
  "task_id": "MAP-030",
  "decision": "revise",
  "summary": "The MAP-030 draft JSON validates against the required schema: all 13 coverage areas are present with status/assessment/source_tasks, six follow-up tasks are proposed with citations and two observable checks each, external_research_required and runtime_tests_required are false everywhere, source_tasks reference only supplied inputs, baseline/proposal modality and unresolved decisions are preserved, and no area is accepted or called build-ready. One correctable omission: the supplied input MAP-015 (docs/map/specs/release-lifecycle.md @ 1cd788bd), covering release lifecycle stages, dependency/schema-migration recording, backup prerequisites, limits of rollback, and a section 10 verification checklist, is not cited anywhere in coverage, tasks, or blockers although its content is relevant to operations (release/rollback reporting) and build-and-acceptance (acceptance-structure input).",
  "findings": [
    "build-and-acceptance and operations coverage omit the supplied MAP-015 input (docs/map/specs/release-lifecycle.md @ revision 1cd788bd): its release lifecycle stages (proposed/reviewed/approved-for-environment/deployed/superseded/withdrawn), dependency-change and data/schema-migration recording, backup prerequisites, limits of rollback, and section 10 verification checklist are directly relevant to acceptance-structure drafting and release/rollback reporting. Correction: cite MAP-015 as unaccepted review material in operations coverage (release/rollback lifecycle and verification context) and build-and-acceptance coverage (its verification checklist as candidate acceptance-structure input), without changing any area status, accepting any area, or treating the checklist as accepted acceptance criteria."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-030",
  "reviewer": "Codex coordinator — current user-authorised correction",
  "at": "2026-10-31T23:06:44.071913+00:00",
  "native_critic_decision": "revise",
  "native_critic_draft_sha256": "1969ff770cb2324500288caea27d44fd359709b1d70adb0fb7c5ae421732c7c1",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Verified pinned MAP-015 at 1cd788bd77c027a6808c3c4179784a77d8ca1efe includes release lifecycle, dependency/schema migration recording, backup prerequisites, rollback limits and Verification Checklist.",
    "Added MAP-015 as an unaccepted source reference in operations and build-and-acceptance assessments; retained all original area statuses and no acceptance/performed-evidence claim.",
    "Declared audit schema validates; original native critic and pre-correction packet are preserved. The new fixed assembly policy consumes existing completed work and ignores audit queue proposals rather than repeatedly generating audits."
  ],
  "checks": [
    "All 13 areas present and declared JSON schema valid",
    "Source references point to supplied immutable inputs",
    "Area statuses unchanged; checklist stays unaccepted/not-performed",
    "No request/correction reset, additional Hermes inference, native recheck, acceptance or merge"
  ],
  "corrected_payload_sha256": "9e6aa65da17f3b251f74082ac4a48dcdca66cddc0193aa064d1051259722cdf4"
}
