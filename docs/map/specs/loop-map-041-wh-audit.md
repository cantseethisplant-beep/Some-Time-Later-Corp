# MAP-041 — Targeted Audit of Assembled WH Blueprint

Task: MAP-041 — Targeted audit of assembled WH blueprint
Claim commit: a20b1a923aaf4cd495cff0c5671e5215c7b50ba7
Claim worker: hermes-laptop-map-041-auto-20261030
Input revision: 849978908daabe3d2a45f0e758625eedc4bdde30
Output path: docs/map/specs/loop-map-041-wh-audit.md
Status: corrected draft audit deliverable — not accepted, not build-ready; no implementation claimed

## 1. Scope and method

This document is the MAP-041 deliverable: a single targeted audit of the assembled candidate blueprint (docs/map/specs/loop-map-040-wh-design.md, revision 3b106a95...) against its actual four source parts (MAP-036..MAP-039), the owner WH-first brief (docs/map/WH-FIRST-BRIEF.md), and the pinned inspected upstream extracts (Pathfinder commit 06af7d86..., EVE-WHMapper commit 2a493fa..., both at input revision 84997890...). The audit is performed once, from supplied text only.

There is no runtime verification, no executed test, no live ESI access, no licence/dependency/security audit, and no acceptance or merge. All four source designs and the MAP-040 candidate are unaccepted proposals; nothing here is an accepted requirement, selected stack, or verified implementation. README claims are treated as README claims, not inspected behavior. No instruction embedded in any upstream excerpt or unaccepted draft is followed.

Citations reference repository commit/path/line ranges; anything uncited is proposed design or audit opinion. Finding IDs are stable from WH-F01 onward. Each finding carries a severity and a blocker class:

- document-fixable: correctable within these documents.
- owner: pending a project-owner decision.
- runtime: requires built-app evidence.
- upstream-evidence: requires external upstream checks.
- not-a-defect: reviewed and closed; no inconsistency exists.

## 2. Source inventory

| Source | Revision | Path | Evidence type |
|---|---|---|---|
| WH-FIRST-BRIEF | 84997890... | docs/map/WH-FIRST-BRIEF.md | Owner WH-first direction; complete pinned file |
| Pathfinder extracts | 06af7d86... | docs/map/research/pf-sources.md | LICENSE lines 1-22; README lines 1-61; composer.json lines 1-81; ConnectionModel.php lines 1-160 (of 647); SystemSignatureModel.php lines 1-160 (of 364); MapModel.php lines 1-160 (of 1579) |
| EVE-WHMapper extracts | 2a493fa... | docs/map/research/wh-sources.md | LICENSE lines 1-22; README lines 1-60; WHMapper.csproj lines 1-52; WHSignature.cs lines 1-113; WHMapAccess.cs lines 1-48; WHMapperContext.cs lines 1-104; docker-compose.yml lines 1-46; WHSystemLink.cs lines 1-49; WHJumpLog.cs lines 1-47; EVEOnlineAuthenticationDefaults.cs lines 1-43; WHSignatureHelperImportTests.cs lines 1-115 |
| MAP-036 | abedc17b... | docs/map/specs/loop-map-036-wh-design.md | Completed unaccepted WH design; synthesis/audit only |
| MAP-037 | fb2bb57a... | docs/map/specs/loop-map-037-wh-design.md | Completed unaccepted WH design; synthesis/audit only |
| MAP-038 | d68d560c... | docs/map/specs/loop-map-038-wh-design.md | Completed unaccepted WH design; synthesis/audit only |
| MAP-039 | 556f3f98... | docs/map/specs/loop-map-039-wh-design.md | Completed unaccepted WH design; synthesis/audit only |
| MAP-040 candidate (audited) | 3b106a95... | docs/map/specs/loop-map-040-wh-design.md | Completed unaccepted candidate; synthesis/audit only |

## 3. Finding register (WH-F01..WH-F16)

| ID | Sev | Class | Candidate section | Evidence/source | Issue | Correction | Verify |
|---|---|---|---|---|---|---|---|
| WH-F01 | Medium | document-fixable | §6 API summary | MAP-037 §5 WH-API-13..16 (instance/bootstrap ops); wh-sources WHMapperContext.cs lines 1-104 | Instance/bootstrap ops (CreateInstance, RegisterActor, TransferOwnership) mixed into the MVP API summary; may imply instance administration is MVP scope. | Move WH-API-13..16 to a separate out-of-MVP subsection; bootstrap actor stays an unresolved owner decision. | Confirm no instance-level op appears in the MVP operations table without an out-of-MVP label. |
| WH-F02 | Medium | owner | §5 R06; §10 | wh-sources 2a493fa... WHMapAccess.cs lines 1-48 (empty list = all instance members); MAP-038 §4, §18 | Candidate adopts explicit-grant-only as default without an owner decision; upstream default is permissive. | Relabel explicit-grant-only as proposed, pending owner decision; cite both behaviors; require owner choice before build acceptance. | Confirm R06 marks explicit-grant-only as proposed/unresolved and cites WHMapAccess.cs lines 1-48. |
| WH-F03 | Medium | document-fixable | §5 R02 | wh-sources 2a493fa... WHSignature.cs lines 1-113 ([StringLength(7)] Name); import tests lines 1-115 (7-char names IGU-360/WAM-436) | Upstream 7-char signature name limit is not carried into the candidate schema. | Add name max-length (proposed 7, owner to confirm) or declare length undecided; do not silently drop the upstream constraint. | Confirm MAP-040 §5 R02 shows a name-length rule or explicit "undecided" marker. |
| WH-F04 | Medium | document-fixable | §6 WH-API-03 behavior; §10 | MAP-037 §5 WH-API-03 (expectedRevision; E_CONCURRENT_REVISION); MAP-039 §3.2 (last-write-wins with activity log) | Conflicting concurrent-edit rules: optimistic revision rejection vs last-write-wins; MAP-040 candidate does not choose between them. | Adopt one stated rule (optimistic revision conflict preferred; last-write-wins only as explicit owner exception with audit entry); remove contradiction from §10 or state it as unresolved. | Confirm a single concurrent-edit rule appears in §6 WH-API-03 behavior and §10, or is explicitly marked pending owner decision. |
| WH-F05 | Low | not-a-defect | §5 R02; §6 signature model | pf-sources 06af7d86... ConnectionModel.php lines 1-160 (signatures has-many from connection); SystemSignatureModel.php lines 1-160 (signature binds to one systemId plus optional connectionId validated to same system); MAP-037 §3 Signature | No defect. Claimed signature/connection cardinality inconsistency does not exist: Pathfinder binds each signature to one system with optional connectionId, and connection-level has-many is a navigation property compatible with the candidate's signature-per-system-with-optional-connectionId design. | None required; close WH-F05 as not-a-defect; remove its residual-unknown cross-reference. | Confirm MAP-040 §5 R02 / §6 describe signature per system with optional connectionId and assert no cardinality contradiction. |
| WH-F06 | High | document-fixable | §6 API summary (WH-API-13..16); §10 | wh-sources 2a493fa... WHMapperContext.cs lines 1-104 (instance ownership and admin tables exist; bootstrap actor unspecified) | WH-API-16 TransferOwnership requires current instance owner but there is no mechanism to designate/create the initial owner without circular bootstrap authority. | Add an explicit "bootstrap actor/initial owner designation is an unresolved owner decision" note under WH-API-13..16; do not imply self-bootstrapping works. | Confirm candidate §6/§10 records bootstrap authority as unresolved and not assumed solvable. |
| WH-F07 | High | document-fixable | §5 R10; §8; §9 | pf-sources README lines 1-61 (backup/migration guidance lives in external pathfinder-containers repo, not in extract); wh-sources docker-compose.yml lines 1-46 (Postgres volume only; no Redis volume evidenced) | No restore-test evidence exists; B06 covers import/export/migration scripts only and does not execute a restore test; the docker-compose extract evidences a Postgres data volume on the db service but no Redis volume. | Restate B06 as scripts only; keep the explicit "backup creation ≠ restore verification" sentence; list no restore-test evidence exists and no Redis volume is evidenced. | Confirm §5 R10 and §8 keep backup creation distinct from restore verification; confirm §9 T09/T10 state backup creation vs tested restore separately; confirm docker-compose note lacks Redis volume evidence. |
| WH-F08 | Medium | owner | §3 | pf-sources composer.json (PHP >=8.2, Fat Free Framework); wh-sources csproj (C# net10.0, EF Core 10.*, PostgreSQL) | Stack alternatives (fork Pathfinder PHP, fork EVE-WHMapper C#, new implementation) remain unresolved; candidate does not state which owner decision unblocks build. | Explicitly state owner stack decision is a prerequisite; list PHP vs C# incompatibility as blocker; no stack selected. | Confirm §3 says owner stack decision pending and no runtime is selected. |
| WH-F09 | High | upstream-evidence | §4; §8; §11 | pf-sources README/security hardening (encrypted ESI tokens at rest with libsodium, 32-byte hex key); wh-sources EVEOnlineAuthenticationDefaults.cs lines 1-43 (revoke endpoint listed, no behavior) | Token storage and revocation are claimed as patterns but runtime behavior (encryption key management, revoke effectiveness, ESI rate limits) is unverified. | Mark auth/token implementation, consent workflow, and revocation effectiveness as explicit blockers; do not present libsodium pattern as adopted implementation. | Confirm candidate §4/§8/§11 lists token storage, revocation, and ESI scopes/rate limits as missing evidence. |
| WH-F10 | Medium | document-fixable | §5 R04; §6 JumpEvidence type | wh-sources WHSignatureHelperImportTests.cs lines 1-115 (scan format: tab-separated; signal examples "100,0%", "100.0%", "42,5%") | MAP-037 §3 JumpEvidence declares shipMass number O >= 0, but the candidate schema (§5 R04 / §6) does not restate the number >= 0 constraint; the negative-mass example is conditionally valid only if that type is confirmed in the candidate. | Restate JumpEvidence.shipMass as number >= 0 in candidate schema; confirm example validates against declared type; note comma decimals are upstream fixtures only, not adopted parsing policy. | Confirm example passes type/range check against declared field type and no decimal-separator policy is silently adopted. |
| WH-F11 | Medium | owner | §5 R07; §11 | wh-sources README lines 1-60 ("automatic location tracking via ESI" — README claim, not verified) | Opt-in tracking default and expiry are undecided; candidate implies tracking exists but no consent workflow is evidenced. | Mark default opt-in state, sharing expiry, and per-jump vs continuous as unresolved owner decisions; no location stored without opt-in. | Confirm §5 R07 and §11 list opt-in default, expiry, and consent workflow as unresolved. |
| WH-F12 | Medium | document-fixable | §6 export/import; §9 | wh-sources WHSignatureHelperImportTests.cs lines 1-115 (dedupe by name+group+type ignoring audit fields) | Tombstone/no-ID-reuse rule is stated but not tied to export re-import validation; second import could duplicate or revive IDs without an import ID/remapping table being operationalized. | Add to §6: import ID/remapping table required; tombstones prevent ID reuse; hard purge admin-only outside MVP; re-import must not duplicate content. | Confirm export section requires remapping table and re-import duplicate prevention. |
| WH-F13 | Medium | document-fixable | §5 R07; §11 | wh-sources EVEOnlineAuthenticationDefaults.cs lines 1-43 (issuer/audience only; no scopes) | Consent model (scope enum map/instance) is proposed but ESI scopes are unspecified; candidate implies consent can be granted without knowing upstream scopes. | Label consent model as proposed; add blocker: ESI scopes, rate limits, issuer contract unknown; no consent workflow evidence. | Confirm §11 blocker #2 lists ESI scopes/rate limits/issuer as unknown and R07 marks consent workflow unevidenced. |
| WH-F14 | Medium | document-fixable | §5 R04; §11 | pf-sources ConnectionModel.php lines 1-160 (JUMP_MASS_BUCKETS S/M/L/Xl thresholds; nominalLifespan) | Candidate references JUMP_MASS_BUCKETS as upstream examples only, but does not state they are not adopted game constants; mass/bucket mapping remains undecided. | Explicitly state JUMP_MASS_BUCKETS are one implementation's inspected constants, not adopted policy; owner must set mass buckets before acceptance. | Confirm R04 or §11 lists mass-bucket mapping as unresolved placeholder. |
| WH-F15 | Medium | document-fixable | §11 blocker #2 | pf-sources composer.json audit ignore entry (PKSA-y2cr-5h3j-g3ys); wh-sources csproj (16+ packages, versions 10.*/18.*/8.22.0) | Dependency inventory lists only root MIT; no transitive dependency, vulnerability, or license-conflict conclusion; audit-ignore entry unexplained. | Add to §11: full dependency licence/security audit for both manifests is missing; audit-ignore entry requires review; no compatibility conclusion drawn. | Confirm §11 blocker #2 covers transitive dependencies for both manifests. |
| WH-F16 | Low | document-fixable | §6 boundaries; §9 | wh-sources docker-compose.yml lines 1-46 (Postgres image postgres:17-alpine; Redis image redis:8-alpine, no volume) | Candidate implies a database but names none; docker-compose shows Postgres only as example deployment, not a mapper prerequisite. | State database engine is undecided; docker-compose is optional background evidence only; no Redis volume evidenced. | Confirm §6 boundaries state DB engine undecided and deployment shape is optional. |

## 4. Schema/example/type/ID consistency checks

Every declared example in MAP-037 §7 (inherited by MAP-040 §6) was checked against the candidate's declared fields:

- Valid Signature update: mapId, requestId, entityType, entityId, expectedRevision, idempotencyKey, patch present; patch touches mutable group/type only; systemId absent so immutable rebinding is not triggered. Passes declared fields/types.
- E_CONCURRENT_REVISION response: ok=false, revision=8, entity present with current authorized fields, errors array with code E_CONCURRENT_REVISION and field expectedRevision. Passes envelope contract.
- E_CROSS_MAP response: ok=false, errors array with code E_CROSS_MAP and field entityId. Passes; E_CROSS_MAP used only after target-map authorization (per MAP-037 §2).
- Negative shipMass example: shipMass:-250000000 returns E_INVALID_PAYLOAD with field shipMass. Passes only if shipMass is declared number >= 0 (see WH-F10).

ID format: UUID canonical text used consistently across examples; no whd- prefix serialized; IDs never reused per tombstone rule. Tombstones remain in history/export; no ID-reuse examples appear. Cross-map isolation is enforced by E_CROSS_MAP after authorization. Authorization failure never reveals entity content beyond an already-addressed entity.

## 5. Duplicate signatures and concurrent/deleted/stale edits

Duplicate signature prevention relies on unique active(mapId,systemId,name) (proposed) plus E_DUPLICATE_SIGNATURE on concurrent creates. Conflicting scans return for review via WH-API-06 with E_CONFLICTING_SCAN. Deletion fails with E_REFERENCED_ENTITY for dependent active references; explicit cascade is not implicit MVP behavior. Stale edits are caught by expectedRevision mismatch returning E_CONCURRENT_REVISION. No example shows a stale edit silently overwriting a newer observation.

WH-F05 was reviewed and closed as not-a-defect: Pathfinder's signature-per-system (systemId) with optional connectionId validated to the same system is compatible with the candidate's signature model; no cardinality contradiction exists. The concurrent-edit policy contradiction (WH-F04) remains the open item.

## 6. Authorization on reads/writes/events and cross-map data

MAP-037 §5 requires authorization before revealing content, before idempotency lookup, and transactionally before applying writes; E_FORBIDDEN never reveals entity existence. WH-API-01 ReadMap returns authorized active entities only with E_FORBIDDEN/E_NOT_FOUND without other-map data. Cross-map binding returns E_CROSS_MAP after target-map authorization. Consent/opt-in is checked on reads/events per MAP-037 §3 Consent (proposed). No handler implementations exist to verify; all authorization claims are proposed design (see WH-F09, WH-F11).

## 7. Consent/revocation/cache privacy

Consent model: actor locationSharingOptIn default false (proposed); Consent entity with scope/targetMapId/optIn/grantedAt/updatedAt (proposed). Revocation: ESI revoke endpoint listed in EVEOnlineAuthenticationDefaults.cs lines 1-43; revocation effectiveness and server-side invalidation unverified (WH-F09). Cache: keys namespaced by instance/map; invalidation on unlink/revocation/membership change proposed; Redis in docker-compose is example only with no volume evidenced (WH-F16). No cache test or invalidation implementation exists.

## 8. Unsafe routing or exact-mass claims

Routing: proposed route planner excludes stale/unknown-mass/denied-access links; ranks fewest hops then fewest wormholes; displays per-leg uncertainty; requires explicit acceptance before sharing. No exact-mass promise; shipMass is estimate only (number >= 0). Pathfinder JUMP_MASS_BUCKETS are inspected examples only, not adopted policy (WH-F14). No hostile-detection or safe-route guarantee appears. Route constants are owner-declared numerics pending verification against authoritative game data (WH-F14, §11).

## 9. MIT attribution and unchecked transitive dependencies

Both roots are MIT (Pathfinder 2017 Mark Friedrich; EVE-WHMapper 2023 pfh59); notices reproduced in pf-sources.md and wh-sources.md LICENSE sections. No substantial upstream block is copied in the design; notice retention obligation applies only if substantial material is copied later. Transitive dependencies are unchecked: Pathfinder composer.json require/require-dev (bcosca/fatfree-core, ikkez/f3-cortex, react/socket, firebase/php-jwt, goryn-clade/pathfinder_esi, phpstan, phpcs, rector, etc.) and EVE-WHMapper csproj PackageReference list (EF Core 10.*, MudBlazor 9.9.0, Npgsql 10.*, OpenTelemetry 1.18.0, SignalR, Serilog, FluentValidation, etc.). Assets (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json) and EVE game data/ESI terms are unchecked (WH-F15). No licence-conflict conclusion between roots is established, but no compatibility conclusion is drawn either.

## 10. Import/export/migration and backup/restore

Export envelope v1 proposed: {format:"wh-export",version:1,sourceInstanceId,sourceMapId,entities,events,snapshotCursor,exportedAt}; secrets excluded; import ID/remapping table required (WH-F12). Migration requires pre-migration backup, migration fixture, rollback procedure — none executed. Backup creation and restore verification are distinct; no restore-test evidence exists; backup is not recovery evidence until a test restore into an empty database passes row-count/content match (WH-F07, WH-F16). docker-compose evidences Postgres data volume only; no Redis volume (WH-F16).

## 11. WH-first versus cloud scope

MVP scope excludes cloud hosting, hardware offers, catalogue deployment, distributed cloud controller; cloud is optional behind clean boundary. WH-API-13..16 instance/bootstrap ops are out of core MVP boundary; bootstrap actor is unresolved owner decision (WH-F01, WH-F06). No cloud module design is admitted into MVP acceptance. Optional hosting work preserved without making it prerequisite.

## 12. Coverage matrix

| Audited area | Source parts | Checked in MAP-041 | Status |
|---|---|---|---|
| Source pins and unsupported upstream claims | All | Commit/path/line citation spot-checks; README vs implementation distinction | Partial — examples validated; unsupported claims flagged |
| WH requirement/step/test crosswalk | MAP-036 R01..R10, MAP-039 B01..B07/T01..T11 | Crosswalked to MAP-040 IDs; no acceptance claimed | Complete for structure only |
| Schema/example/type/ID consistency | MAP-037 §3/§7 | All four examples checked | Complete; WH-F10 type clarification needed |
| Duplicate signatures and concurrent/deleted/stale edits | MAP-037 §4/§5/§6 | Rules reviewed; WH-F05 closed not-a-defect; WH-F04 open | Partial |
| Authorization reads/writes/events and cross-map data | MAP-037 §5; MAP-038 §11/§17 | Contract reviewed; no implementation evidence | Partial |
| Consent/revocation/cache privacy | MAP-037 §3/§6; MAP-038 §7/§14 | Model proposed; ESI scopes unknown | Partial |
| Unsafe routing/exact-mass claims | MAP-039 §3.4/§3.5 | No exact-mass or safe-route claims found | Complete (negative finding) |
| MIT attribution/transitive dependencies | MAP-040 §4; pf/wh LICENSE | Root licences confirmed; transitive unchecked | Partial |
| Import/export/migration/backup/restore | MAP-037 §6; MAP-039 §5.4 | Backup vs restore distinct; no restore evidence | Complete (negative evidence) |
| WH-first vs cloud scope | WH-FIRST-BRIEF; MAP-040 §1/§5 | Cloud excluded from MVP; bootstrap unresolved | Complete |

## 13. Tests of examples actually checked

| Example | Location | Required fields present | Types/range honored | Result |
|---|---|---|---|---|
| Valid Signature update (WH-API-03) | MAP-037 §7 | Yes (mapId, requestId, entityType, entityId, expectedRevision, idempotencyKey, patch) | patch mutable fields only | Pass |
| E_CONCURRENT_REVISION | MAP-037 §7 | Yes (ok, revision, entity, errors[].code, errors[].field) | revision integer; entity authorized-current | Pass |
| E_CROSS_MAP | MAP-037 §7 | Yes (ok, errors[].code/field) | E_CROSS_MAP post-authorization | Pass |
| Negative shipMass (WH-API-02) | MAP-037 §7 | Yes (connectionId, characterActorId, jumpDate, source, idempotencyKey, shipMass) | shipMass must be >= 0 if declared number | Conditional pass (see WH-F10) |

No runtime tests executed. Decimal separators ("100,0%" vs "100.0%") are upstream fixtures only; no parsing policy adopted.

## 14. Residual unknowns

1. Target language/runtime/stack decision (PHP Pathfinder fork vs C# EVE-WHMapper fork vs new implementation) — owner decision (WH-F08).
2. ESI scopes, rate limits, issuer runtime contract; consent workflow evidence missing (WH-F09, WH-F11, WH-F13).
3. Full dependency licence/security audit for composer.json and csproj; audit-ignore entry review (WH-F15).
4. Asset licence check (favicon/logo; wh-effects.json); EVE game data/ESI terms-of-use check (WH-F15).
5. Numeric stale threshold, mass-bucket mapping, route-constraint values — owner placeholders (WH-F14).
6. Auth/token-storage implementation; encrypted-at-rest pattern not adopted; revocation effectiveness unverified (WH-F09).
7. Restore-test evidence missing; backup creation ≠ restore verification (WH-F07, WH-F16).
8. Unseen handler implementations; per-handler authorization must be implemented and tested (runtime).
9. Bootstrap actor/initial owner designation mechanism missing (WH-F06).
10. Concurrent-edit rule conflict between MAP-037 and MAP-039 unresolved (WH-F04).
11. Signature name max-length (7 upstream) undecided in candidate schema (WH-F03).
12. Database engine undecided; docker-compose Postgres is example only (WH-F16).

## 15. Handoff summary

MAP-041 completes one targeted audit of the assembled candidate against its four source parts, brief, and pinned extracts. Sixteen findings (WH-F01..WH-F16) are registered: 11 document-fixable (WH-F01, WH-F03, WH-F04, WH-F06, WH-F07, WH-F10, WH-F12, WH-F13, WH-F14, WH-F15, WH-F16), 3 owner decisions (WH-F02, WH-F08, WH-F11), 1 upstream-evidence block (WH-F09), and 1 not-a-defect (WH-F05); no ID appears in two classes. All examples checked pass structurally; one conditional pass on shipMass type (WH-F10). No implementation, acceptance, merge, or certification is claimed. The candidate remains a draft for review. Residual unknowns and blockers are listed above; none are repaired by invention.
