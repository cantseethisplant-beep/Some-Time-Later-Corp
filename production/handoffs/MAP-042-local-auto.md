# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/36

Automated critic only; independent review pending.

# Coordinator recovery handoff — MAP-042

Task: MAP-042; claim commit: 5352b3a4d910ef1e373fe839f90f96ecdd521414  
Output path: docs/map/specs/loop-map-042-wh-design.md  
Status: draft candidate for review — not accepted, not merged, not build-ready, no implementation claimed  
WH version: 1, WH stage: 7, loop policy: 1, loop kind: wh-design

## Sources verified (pinned inputs only)
- docs/map/WH-FIRST-BRIEF.md @ 849978908daabe3d2a45f0e758625eedc4bdde30
- docs/map/research/pf-sources.md @ 849978908daabe3d2a45f0e758625eedc4bdde30
- docs/map/research/wh-sources.md @ 849978908daabe3d2a45f0e758625eedc4bdde30
- docs/map/specs/loop-map-036-wh-design.md @ abedc17bddc7f573f434f4dad78969471b9f3c9e
- docs/map/specs/loop-map-037-wh-design.md @ fb2bb57a8f28f5362912f6c4a94d5845dbaabd2a
- docs/map/specs/loop-map-038-wh-design.md @ d68d560c9f6687f96bf82de8a980b13c385a7f2b
- docs/map/specs/loop-map-039-wh-design.md @ 556f3f983f9b1d3b2b3acc20853bcfd18c797348
- docs/map/specs/loop-map-040-wh-design.md @ 3b106a956ed936af87f80ffcc293741ebf9303bc
- docs/map/specs/loop-map-041-wh-audit.md @ fa913fc258b0b459e57499220ef31476a6f392bc

## Diagnosed issues from prior draft and exact corrections
1. Canonical finding-ID scheme declared in §2 (WH-042-Fxx) but never applied; §12/§13 used WH-F01..WH-F16 only. Corrected: retained original WH-F IDs unchanged throughout §12 and §13; §2 crosswalk lists them as traceable without inventing a second scheme.
2. §6 example 4 cited nonexistent MAP-041 finding "WH-F041-10". Corrected: cites MAP-041 WH-F10 (shipMass type finding).
3. Internal section cross-references wrong: §5 R02/R06/R07 notes and §12 rows WH-F02/WH-F03/WH-F11 cited non-existent "§11 item 10/12/13". Corrected: re-pointed directly to §15 items 10/12/13.
4. §12 row WH-F01 cited §15 item 9 (bootstrap actor, which belongs to WH-F06). Corrected: WH-F01 now references §6 WH-API-13..16 note; bootstrap actor reference consolidated under §15 item 9 (WH-F06).

## Checks actually performed
- Re-read all pinned input files at declared revisions; no OCR or extraction needed (plain-text sources supplied).
- Cross-checked MAP-041 findings WH-F01..WH-F16 against MAP-040 candidate sections and applied 14 source-answerable corrections listed in §13.
- Verified every declared JSON example in §6 against required fields, types, ID format (UUID canonical text, no whd- prefix), tenant scope, and error definitions; example 4 is conditional on JumpEvidence.shipMass declared `number >= 0` (WH-F10).
- Confirmed backup creation vs restore verification is kept distinct; no restore-test claim made; docker-compose Postgres-only volume evidence verified, no Redis volume claimed.
- Confirmed both root MIT licences reproduced; notice obligation scoped to substantial copies only.
- Confirmed WH-first scope preserved; cloud optional behind clean boundary; no stack selected; no code implemented; no tests executed.

## Limitations
- No GitHub, terminal, network, or delegation tools available; no runtime verification, no live ESI access, no dependency/security audit, no executed tests.
- All upstream extracts are inspected source only; README claims treated as claims, not verified behavior.
- Word-count aim (1200–1800 words) is a target, not a substantive acceptance gate.

## Remaining work / review pending
- Independent project owner review of the candidate blueprint.
- Resolution of the 14 owner/evidence decisions listed in §15 (stack decision, ESI scopes/rate limits, dependency/asset/game-data licence checks, stale threshold, mass buckets, auth/token implementation, restore-test evidence, bootstrap mechanism, signature name length, explicit-grant default, opt-in defaults).
- Per-handler authorization implementation and testing once the app is built.
- Formal acceptance and merge remain outside this task; no self-acceptance or build-ready certification claimed.

## Evidence status
All sources labelled with actual evidence status; completed unaccepted drafts (MAP-036..MAP-041) used for synthesis/audit only, not accepted requirements or performed technical evidence.


## Explicit final Codex coordinator completion
- Corrected bootstrap/signature-length/access-default/opt-in decision references in sections 5, 11, 12 and 13 against the actual section 15 register; added stable OD identifiers.
- Expanded abbreviated UUID examples; clarified proposed responses, tenant/map ownership, signature identity, exact error name and source-copy notice wording; added the missing MAP-040 source inventory row.
- Added an explicit prerequisite-ordered build plan with baseline/bootstrap and early permission gates; separated offline local proposals from accepted server writes.
- Added requirement-to-build/test traceability for all ten requirements, six missing observable check specifications, and scope notes for inherited security tests; no tests marked executed.
- All 14 stable OD identifiers resolve and section-15 item pairs agree
- All ten requirements map to build steps and observable checks
- All 16 audit findings appear exactly once in disposition table
- 5 JSON examples parse; identifier fields are complete canonical UUIDs
- Known bad decision/section/error references removed
- Proposed design, independent acceptance and runtime-evidence boundaries preserved
No fresh native critique, project acceptance, implementation or runtime test. Original source and critic history retained.

## Automated screening
{
  "task_id": "MAP-042",
  "decision": "revise",
  "summary": "The draft retains WH-F01..WH-F16, applies the 14 source-answerable corrections, keeps all proposals unaccepted, preserves WH-first scope, and separates document checks from future runtime tests. Its remaining defects are systematic off-by-one cross-references to the §15 owner/evidence decisions: bootstrap actor/initial owner designation is §15 item 10 (rows cite item 9, which is unseen handler implementations), signature name max-length is §15 item 11 (rows cite item 10), explicit-grant-only default is §15 item 13 (rows cite item 12), and opt-in defaults are §15 item 14 (rows cite item 13). The mis-citations occur in §5 notes (R02/R06/R07), §11 open-decisions list, §12 disposition rows (WH-F01, WH-F02, WH-F03, WH-F06, WH-F11), and §13 corrections (#3, #4, #9). Each must be repointed to its exact §15 item so remaining decisions are precise and traceable.",
  "findings": [
    "§5 requirement notes cite wrong §15 owner-decision items: WH-042-R02 note (signature name max-length) cites §15 item 10 but item 10 is bootstrap actor/initial owner designation (WH-F06); signature name max-length is §15 item 11 (WH-F03). WH-042-R06 note (explicit-grant-only default) cites §15 item 12 but item 12 is database engine undecided (WH-F16); explicit-grant-only default is §15 item 13 (WH-F02). WH-042-R07 note (opt-in defaults) cites §15 item 13 but item 13 is explicit-grant-only default (WH-F02); opt-in defaults are §15 item 14 (WH-F11). Correction: repoint §5 R02 to item 11, §5 R06 to item 13, §5 R07 to item 14.",
    "§11 open owner-decisions list mis-cites §15 items: \"item 10 signature name max-length (§15 item 10)\" but signature name max-length is §15 item 11; \"item 12 explicit-grant-only default (§15 item 12)\" but it is §15 item 13; \"item 13 opt-in defaults (§15 item 13)\" but opt-in defaults are §15 item 14. Correction: repoint to §15 items 11, 13, 14 respectively.",
    "§12 audit disposition rows mis-cite §15 items: WH-F01 and WH-F06 cite §15 item 9 for bootstrap actor/initial owner designation, but item 9 is unseen handler implementations; bootstrap actor is §15 item 10. WH-F02 cites §15 item 12 for explicit-grant-only default; should be item 13. WH-F03 cites §15 item 10 for signature name max-length; should be item 11. WH-F11 cites §15 item 13 for opt-in defaults; should be item 14. Correction: repoint WH-F01/WH-F06 to item 10, WH-F02 to item 13, WH-F03 to item 11, WH-F11 to item 14.",
    "§13 applied-corrections list mis-cites §15 items: correction #3 (explicit-grant-only default, WH-F02) cites §15 item 12; should be item 13. Correction #4 (signature name max-length, WH-F03) cites §15 item 10; should be item 11. Correction #9 (opt-in defaults, WH-F11) cites §15 item 13; should be item 14. Correction: repoint #3 to item 13, #4 to item 11, #9 to item 14."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-042",
  "reviewer": "Codex coordinator — explicit owner-requested final WH blueprint completion",
  "at": "2026-11-02T13:10:00.240658+00:00",
  "native_critic_decision": "revise",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Corrected bootstrap/signature-length/access-default/opt-in decision references in sections 5, 11, 12 and 13 against the actual section 15 register; added stable OD identifiers.",
    "Expanded abbreviated UUID examples; clarified proposed responses, tenant/map ownership, signature identity, exact error name and source-copy notice wording; added the missing MAP-040 source inventory row.",
    "Added an explicit prerequisite-ordered build plan with baseline/bootstrap and early permission gates; separated offline local proposals from accepted server writes.",
    "Added requirement-to-build/test traceability for all ten requirements, six missing observable check specifications, and scope notes for inherited security tests; no tests marked executed."
  ],
  "checks": [
    "All 14 stable OD identifiers resolve and section-15 item pairs agree",
    "All ten requirements map to build steps and observable checks",
    "All 16 audit findings appear exactly once in disposition table",
    "5 JSON examples parse; identifier fields are complete canonical UUIDs",
    "Known bad decision/section/error references removed",
    "Proposed design, independent acceptance and runtime-evidence boundaries preserved"
  ],
  "corrected_payload_sha256": "14a62974994b90aa68eb5c4396fcf139e15d3aa5408256180cf2c55d69934154"
}
