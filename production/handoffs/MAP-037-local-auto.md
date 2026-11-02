# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/33

Automated critic only; independent review pending.

## MAP-037 Draft Handoff (corrected)

Task: MAP-037 — WH data, API and concurrent map synchronization contract
Worker: hermes-laptop-map-037-auto-20261030
Claim commit: d710bacb413c73a012d94a2254c857b0cf2675c8
Claim token: 2hTRCIb7eal9xIbek9dILyhwCOK9f_9j
Input revision: 849978908daabe3d2a45f0e758625eedc4bdde30
Output path: docs/map/specs/loop-map-037-wh-design.md (complete plain-text file section above)

Diagnosed issues and exact corrections:
1. Section 4 required reappearing signatures to link to an old tombstone via supersedesSignatureId, but Section 3 declared no such field on Signature. Correction: added `supersedesSignatureId UUID O` to the Signature entity row in section 3, with invariants that it references a Signature tombstone on the same map, never self-references, and never revives an old ID; section 4's linking rule now cites that declared field.
2. Section 5 WH-API-14 CreateMap authorized "instance owner/mapAdmin", but mapAdmin is a per-map grant (unique(mapId,actorId)) that cannot exist before map creation. Correction: WH-API-14 actor is now "instance owner/instance admin", bootstrap authorization is marked as an unresolved owner decision, and the row explicitly notes that mapAdmin cannot pre-exist map creation.

Inputs used (immutable pinned revision 849978908daabe3d2a45f0e758625eedc4bdde30):
- docs/map/WH-FIRST-BRIEF.md (owner WH-first direction)
- docs/map/research/pf-sources.md (Pathfinder commit 06af7d86fe6456947fb960220c54d02a8623c0ff: LICENSE, README, composer.json, ConnectionModel.php lines 1-160 of 647, SystemSignatureModel.php lines 1-160 of 364, MapModel.php lines 1-160 of 1579)
- docs/map/research/wh-sources.md (EVE-WHMapper commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: LICENSE, README, WHMapper.csproj, WHSignature.cs lines 1-113 of 113, WHMapAccess.cs lines 1-48 of 48, WHMapperContext.cs lines 1-104 of 104, WHSystemLink.cs lines 1-49 of 49, WHJumpLog.cs lines 1-47 of 47, EVEOnlineAuthenticationDefaults.cs lines 1-43 of 43, WHSignatureHelperImportTests.cs lines 1-115 of 115)

Remaining uncertainty:
- Stack/language selection unresolved; no owner-approved stack is selected and PHP vs C# vs other is not decided.
- Exact numeric policies (mass buckets, EOL ages, signal thresholds, signature length limits) pending authoritative game/API data; Pathfinder JUMP_MASS_BUCKETS thresholds are cited as inspected upstream examples only, not adopted policy.
- Cloud module boundary, authentication implementation beyond CCP SSO direction, route planner algorithm, and opt-in pilot/location tracking scope are not finalized.
- Bootstrap/instance-creation actor is an owner decision; no live EVE API validation, runtime test evidence, dependency/licence/security audit beyond the two inspected MIT roots, or restore verification procedure has been performed.

Checks actually performed:
- Distinguished baseline intent (WH-FIRST-BRIEF) from new proposed schema rules; all proposed items are labelled as proposals; unresolved policy is not used as a mandate in examples.
- Extracted field types, nullability, FK ownership and uniqueness constraints from inspected upstream lines; cited commit/path/line ranges inline (Pathfinder ConnectionModel.php/SystemSignatureModel.php/MapModel.php; EVE-WHMapper WHSignature.cs/WHMapAccess.cs/WHMapperContext.cs/WHSystemLink.cs/WHJumpLog.cs).
- Preserved optional/required distinctions: Pathfinder active default 1 vs allowUnknownSystems default 0; EVE-WHMapper required Name vs optional Type; HasSameContent null-type == empty-type semantics; only 100% signal variants count as fully scanned per import tests.
- Checked every example against required fields: valid signature update contains all declared payload fields; invalid examples use only declared stable error codes (E_INVALID_PAYLOAD, E_CONCURRENT_REVISION, E_CROSS_MAP); no undeclared error code such as E_INVALID_FULLY_SCANNED is mandated.
- Labelled unaccepted proposals: duplicate/reappearing signature rules, conflicting scans, tombstones, export versioning, reconnect/replay, idempotency keys, revision tokens, cross-map isolation, consent modelling, tenant-root admin operations.
- Applied the two critic corrections listed above (supersedesSignatureId declaration; CreateMap actor correction).
- Identified unresolved owner decisions: stack, numeric policies, cloud boundary, authentication details, bootstrap actor.

Limitations:
- No GitHub, terminal, network, delegation or tool access; no runtime verification, licence/security audit, dependency check, or live EVE API validation.
- No implementation code, no selected stack, no acceptance, no merge, no deployment.
- Word-count aim is a drafting target, not a substantive acceptance gate; output is draft review material only.

Remaining work / review pending:
- Owner review of proposed entity dictionary, CRUD/sync operations, conflict rules, consent model and tenant-root admin boundary.
- Owner decisions on stack, numeric policies, cloud boundary, authentication details and bootstrap actor.
- Independent acceptance and completion gate before any integration; this document is not build-ready.


## Deterministic example repair
Deterministic wh-negative-mass-example-idempotency-v1: added a synthetic required idempotencyKey to the sole diagnosed negative-mass request fixture. Original request fields and deliberate negative shipMass unchanged. Native critic requested revision; corrected fixture passed only this narrow JSON/envelope check, without another native inference or project acceptance.

## Automated screening
{
  "task_id": "MAP-037",
  "decision": "revise",
  "summary": "Section 7's invalid WH-API-02 JumpEvidence create example omits idempotencyKey, which Section 5 requires for mutations, so the example cannot cleanly isolate the shipMass E_INVALID_PAYLOAD check; add idempotencyKey to that request.",
  "findings": [
    "Section 7 invalid WH-API-02 example: the JumpEvidence create request is missing idempotencyKey (required for mutations per Section 5) while only declaring shipMass:-250000000 as the defect, so it cannot demonstrate ship-mass validation in isolation; correction: add \"idempotencyKey\":\"jump-evidence-create-502\" to the request, keeping expectedRevision absent since it applies only to existing entities."
  ],
  "deterministic_correction": {
    "task_id": "MAP-037",
    "run": "eve-blueprint-20261030",
    "rule": "wh-negative-mass-example-idempotency-v1",
    "original_payload_sha256": "57f8015f9d0d8b499d88eb098d6fb778eeb6e4e95bcb5031675180c676f6a46f",
    "corrected_payload_sha256": "c35aeaa6ae1e81dceb0e51a21e363a41cfb01599303b17e4f4edcf47358064e7",
    "native_rechecked": false,
    "accepted": false,
    "checks": [
      "sole current native finding matches allowlisted defect",
      "declared mutation envelope requires key",
      "UUIDs and JSON parsed",
      "only synthetic idempotency key added; original fields and negative mass preserved"
    ],
    "at": "2026-11-02T08:14:15.483651+00:00"
  }
}
