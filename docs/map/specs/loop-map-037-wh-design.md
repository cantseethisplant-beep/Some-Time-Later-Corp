# LOOP-MAP-037 — WH Data, API and Concurrent Map Synchronization Contract

**Status:** proposed draft — unaccepted, not build-ready. MAP-037 output only; not acceptance, implementation, or stack selection.

## 1. Purpose, scope and evidence frame

This draft specifies local identifiers WH-D (data/domain layer) and WH-API (client-facing API/sync surface), a proposed entity dictionary, CRUD/import/sync operations, concurrency and conflict rules, export versioning, and residual blockers for the wormhole-first mapping/intel/operations tool directed by docs/map/WH-FIRST-BRIEF.md (repository revision 849978908daabe3d2a45f0e758625eedc4bdde30).

WH-first scope from the brief: shared system/connection chain map; probe-signature paste/import/edit/history; timestamps and stale observations; observed hole life/size/mass and jump evidence; route planning over mapped connections; per-map permissions; opt-in pilot/location tracking; basic notes and observed intel; corporation administration; backup/export/import and release recovery. Cloud hosting is an optional module behind a clean boundary and is not part of this contract.

Baseline intent (brief, not technical evidence): observations, jump logs, mass estimates and user intel retain source/time/uncertainty; the tool must not promise complete hostile detection, guaranteed safe routes, exact remaining mass, perfect location polling or unobserved activity; numeric policies and API details must be checked later against authoritative game/API data.

New proposed schema rules (this draft, labelled as such): WH-D/WH-API namespaces, stable ID shape, revision tokens, tombstones, per-map event log, idempotency keys, cross-map isolation, export envelope versioning, consent modelling, supersedesSignatureId linking. None are accepted requirements.

Evidence limit: the only upstream inputs are pinned inspected excerpts at revision 849978908daabe3d2a45f0e758625eedc4bdde30:
- Pathfinder commit 06af7d86fe6456947fb960220c54d02a8623c0ff: LICENSE, README, composer.json, app/Model/Pathfinder/ConnectionModel.php lines 1-160 (of 647), app/Model/Pathfinder/SystemSignatureModel.php lines 1-160 (of 364), app/Model/Pathfinder/MapModel.php lines 1-160 (of 1579).
- EVE-WHMapper commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: LICENSE, README, src/WHMapper/WHMapper.csproj, src/WHMapper/Models/Db/WHSignature.cs lines 1-113 (of 113), src/WHMapper/Models/Db/WHMapAccess.cs lines 1-48 (of 48), src/WHMapper/Data/WHMapperContext.cs lines 1-104 (of 104), src/WHMapper/Models/Db/WHSystemLink.cs lines 1-49 (of 49), src/WHMapper/Models/Db/WHJumpLog.cs lines 1-47 (of 47), src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1-43 (of 43), src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115 (of 115).

These extracts establish only file contents; they are not runtime verification, a licence/dependency/security audit, or compatibility evidence. Both inspected roots are MIT; copyright and permission notices must be retained for any copied substantial material. Dependencies, assets and game data require separate checks. No EVE API access, live validation, paid service, or implementation is claimed.

## 2. Proposed identifiers, ownership and common fields

All following contracts are new proposals, not assertions of upstream behavior. WH-D names entities and WH-API names logical operations. The identifier type is UUID serialized as canonical UUID text; the storage/generation algorithm is undecided; no whd- prefix is serialized. IDs are never reused, including after deletion; see section 6. IDs crossing an instance boundary are forbidden. Referencing the wrong map returns E_CROSS_MAP only after authorization to the addressed map has succeeded; otherwise E_FORBIDDEN does not reveal entity existence.

The instance is the tenant root. Maps belong to an instance. Systems/connections/signatures/observations/jump evidence/notes belong to one map. Actors belong to an instance and receive explicit per-map grants; actors are not owned by one map.

Common map-owned record fields: immutable entity ID UUID; mapId UUID required; revision integer >= 1, server-set; active boolean server-set, initially true; createdAt/updatedAt UTC timestamps server-set; createdBy/updatedBy actor UUID required. Instances, maps and actors have corresponding revision/audit fields and instance ownership instead of a mapId where inapplicable. These common fields are inherited by every entity below. Foreign keys and mutations validate ownership atomically. Actor identity is derived from the authenticated session, never trusted from request data.

## 3. Proposed entity dictionary and invariants

R means required/non-null; O nullable; server-set fields cannot be assigned by clients. No numeric game constant or automatic deletion threshold is adopted.

| WH-D entity | Specific fields, types and invariants (in addition to common fields) |
|---|---|
| Instance | instanceId UUID R primary key; name string R; ownerActorId UUID R; tenant root, no mapId |
| Map | mapId UUID R primary key; instanceId UUID R; name string R, unique within instance; no parent mapId |
| Actor | actorId UUID R primary key; instanceId UUID R; eveCharacterId integer O; displayName string R; locationSharingOptIn boolean R default false (proposed consent field); no mapId; character-link verification and identity linking remain authentication prerequisites |
| Consent (proposed) | consentId UUID R primary key; actorId UUID R same instance; scope enum map/instance R; targetMapId UUID O, same map when scope=map; optIn boolean R default false; grantedAt/updatedAt server-set; unique(actorId,scope,targetMapId); grants and opt-in checked on reads and events, not only writes |
| Grant | grantId UUID R; instanceId/mapId/actorId UUID R; role enum viewer/editor/mapAdmin; unique(mapId,actorId); role changes require authorized mapAdmin; initial owner grant created with map; cannot revoke last administrator without explicit owner transfer |
| System | systemId UUID R primary key; eveSystemId integer O; name string R; classLabel string O; unique(mapId,eveSystemId) when known; external universe identity validation pending authoritative game data |
| Connection | connectionId UUID R primary key; sourceSystemId/targetSystemId UUID R, distinct and same map, immutable post-create; holeType/sizeLabel/massStatus/lifeStatus string O; statusObservedAt UTC O paired with statusSource string O; nominalLifespan integer O >= 0, unit/authority unresolved; repeated endpoint pairs allowed because connection ID, not endpoint pair, identifies an observed hole; no exact remaining-mass promise |
| Signature | signatureId UUID R primary key; systemId UUID R same map, immutable post-create; connectionId UUID O, connection must have that system as an endpoint; supersedesSignatureId UUID O, references a Signature tombstone on the same map when a signature reappears; never self-references and never revives an old ID; name string R; group/type/signalText string O; fullyScanned boolean R computed from reviewed parser policy; unique active(mapId,systemId,name), independent of group/type |
| Observation | observationId UUID R primary key; systemId/connectionId UUID O, exactly one set and same map; observedAt UTC R; source string R; uncertainty string O; expiresAt UTC O > observedAt; observedAt supplied by authenticated observer, recordedAt is common createdAt; future/unreasonable timestamps rejected under a documented clock-tolerance policy still to be chosen |
| JumpEvidence | jumpId UUID R primary key; connectionId UUID R same map; characterActorId UUID R within instance and authorized/consented for sharing; jumpDate UTC R; source string R; uncertainty string O; shipTypeId integer O; shipItemId integer O; shipMass number O >= 0, estimate only; no assertion that ESI supplies a jump-log feed |
| Note | noteId UUID R primary key; systemId UUID O same map; content string R; optional proposed 512-character UI limit, to be reconciled with the UI specification; no unique(mapId,systemId) constraint so multiple observations may be recorded |

A location observation identifies a system but does not disclose an actor location unless that actor has opted in to this map's sharing policy. Access and consent must be checked on reads/events, not only writes. Observation expiry marks data stale; it does not prove a hole collapsed or erase history. Missing life/mass/source information remains unknown.

Immutable post-create (proposed): Instance.instanceId, Map.mapId, Actor.actorId, Signature.systemId, Connection.sourceSystemId and Connection.targetSystemId. Moving an existing signature to another system is E_INVALID_PAYLOAD, preserving its identity/history.

## 4. Duplicate signatures, reappearance and conflicting scans

The identity key is the map/system/signature name; group/type are mutable content, never a second identity key. Identical imports are no-ops (no revision increment); conflicting content is returned for explicit review. Two concurrent creates for one key yield one active row, enforced transactionally, and E_DUPLICATE_SIGNATURE on the other create. Conflicting scans do not silently overwrite a newer observation. Provenance and prior content remain in events. A reappearance creates a new signature ID linked by proposed supersedesSignatureId to the old tombstone, rather than reviving/reusing a deleted ID; old history stays immutable. Detection of whether a repeated name is truly the same site remains an observation uncertainty, not a claimed game rule.

The inspected import tests include decimal separators and partial versus full-signal examples; this informs future parser fixtures, not an assertion that an uninspected implementation or a new game rule has been verified. Fully-scanned policy and accepted scan formats must be checked against authoritative current data before build acceptance. An import preview returns normalized rows, warnings/conflicts and a preview hash; commit validates the preview hash and expected revisions again. No destructive deletion merely because a signature is absent from one paste.

## 5. WH-API logical operation contract

All operations are proposed logical operations, not deployed HTTP routes. The server derives the actor from a validated session. Each request contains target mapId (or instanceId for instance/map/actor administration), requestId UUID and only its declared payload. Mutations require idempotencyKey string and expectedRevision for existing entities. Authorization is checked before revealing entity content, before idempotency-cache lookup, and again transactionally before applying a write. Cache keys bind tenant, map, actor, operation, key and payload hash; replaying a key with another payload gives E_IDEMPOTENCY_CONFLICT. Repeats return the original authorized result without new side effects; cache retention is an explicit unresolved operational policy.

| Stable operation | Actor and input | Result and failure contract |
|---|---|---|
| WH-API-01 ReadMap | viewer; mapId, optional entity filters | authorized active entities plus revision/cursor; E_FORBIDDEN or E_NOT_FOUND without other-map data |
| WH-API-02 CreateEntity | editor; mapId, entityType and entity fields | entity, revision=1 and committed event; E_INVALID_PAYLOAD, E_CROSS_MAP, E_DUPLICATE_SIGNATURE; create map itself uses WH-API-14 |
| WH-API-03 UpdateEntity | editor; mapId, entityType, entityId, expectedRevision, patch | updated entity/revision/event; E_CONCURRENT_REVISION with authorized current entity, E_INVALID_PAYLOAD, E_CROSS_MAP; immutable-system rebinding is E_INVALID_PAYLOAD |
| WH-API-04 DeleteEntity | editor; mapId, entityType, entityId, expectedRevision | tombstone and event; deletes with dependent active references fail E_REFERENCED_ENTITY; explicit separately reviewed cascade is not implicit MVP behavior |
| WH-API-05 PreviewScan | editor; mapId, systemId, scanText | normalized rows, previewHash, proposed changes and conflicts; no persistent mutation; E_INVALID_PAYLOAD/E_CROSS_MAP |
| WH-API-06 CommitScan | editor; mapId, systemId, previewHash, normalized rows, expected revisions | counts, committed entities/events, conflicts; transactional ownership/duplicate/revision checks; stale preview E_CONCURRENT_REVISION; E_CONFLICTING_SCAN for unresolved content |
| WH-API-07 PullEvents | viewer; mapId, lastSequenceNo | ordered authorized events and new cursor; E_CURSOR_EXPIRED requires authorized snapshot plus cursor reset; cursor ahead of server E_INVALID_CURSOR; never request nonexistent future events |
| WH-API-08 PushMutations | editor; mapId, mutation list with operation IDs, expected revisions and individual idempotency keys | per-mutation results, sequence numbers and cursor; each mutation atomic, explicit partial-result semantics; no hidden all-or-nothing batch promise |
| WH-API-09 ExportMap | mapAdmin; mapId | versioned authorized export excluding credentials; consent/visibility checked for personal evidence; E_FORBIDDEN |
| WH-API-10 ValidateImport | mapAdmin; mapId, export envelope | schema/ownership/conflict report, import preview hash; no mutation; E_UNSUPPORTED_VERSION/E_INVALID_PAYLOAD |
| WH-API-11 CommitImport | mapAdmin; mapId, validated import hash, target revision | all-or-nothing import transaction with identity remapping; E_CONCURRENT_REVISION/E_IMPORT_CONFLICT; grants/actors/credentials not implicitly imported |
| WH-API-12 ManageGrant | mapAdmin; mapId, targetActorId, role or revoke, expected grant revision | revised grant, authorization-change event; cannot revoke last administrator without explicit owner transfer; E_FORBIDDEN/E_INVALID_PAYLOAD |
| WH-API-13 CreateInstance | bootstrap actor; name, ownerActorId | instance, initial owner actor/grant; E_INVALID_PAYLOAD; instance creation is out of routine MVP scope |
| WH-API-14 CreateMap | instance owner/instance admin; instanceId, name | map with initial owner grant; E_FORBIDDEN, E_INVALID_PAYLOAD, E_DUPLICATE (map name unique within instance); bootstrap authorization is an unresolved owner decision because mapAdmin is a per-map grant that cannot exist before map creation |
| WH-API-15 RegisterActor | instance admin; instanceId, displayName, eveCharacterId O | actor; E_INVALID_PAYLOAD |
| WH-API-16 TransferOwnership | current instance owner; instanceId, newOwnerActorId | updated ownerActorId and grant; E_FORBIDDEN if not current owner |

Tenant-root operations WH-API-13 to WH-API-16 are explicitly proposed and out of the core map MVP boundary; the brief leaves instance setup to corporation administration, so who performs bootstrap remains an owner decision.

Every accepted mutation atomically commits entity revision and an event {eventId: UUID, mapId: UUID, sequenceNo: integer, entityId: UUID, revision: integer, eventType: string, payload: object, actorId: UUID, occurredAt: UTC}. Per-map sequence ordering and event ID uniqueness prevent duplicate application. Reconnect resumes from last acknowledged cursor; if history was compacted, obtain one authorized snapshot with its associated cursor, then replay newer events. A gap requires replay/snapshot, not silently skipping. Revoked clients receive no further private event payload; reconnect rechecks grants and consent. Offline edits are proposals until the server reauthorizes and validates current revisions.

Stable result envelope: {ok: boolean, entity?: object, revision?: integer, events?: array, cursor?: integer, errors?: [{code: string, message: string, field?: string}]}. Specific operation results add only their declared fields (scan counts/conflicts, previewHash or export envelope). Error codes: E_FORBIDDEN, E_NOT_FOUND, E_INVALID_PAYLOAD, E_CROSS_MAP, E_CONCURRENT_REVISION, E_DUPLICATE, E_DUPLICATE_SIGNATURE, E_REFERENCED_ENTITY, E_IDEMPOTENCY_CONFLICT, E_INVALID_CURSOR, E_CURSOR_EXPIRED, E_UNSUPPORTED_VERSION, E_IMPORT_CONFLICT, E_CONFLICTING_SCAN. Authorization failure never includes the current entity or cached private response.

## 6. Export versioning, tombstones and migration boundary

Proposed envelope v1: {format: "wh-export", version: 1, sourceInstanceId, sourceMapId, entities, events, snapshotCursor, exportedAt}. Every entity retains source IDs and revision/provenance. Secrets, tokens and session/idempotency-cache data are excluded. Grant/actor references require explicit authorized target mappings; importing a file cannot grant access. Validate all references and version before applying anything, and use an import ID/remapping table so a second import cannot duplicate content or revive another tenant's IDs.

IDs are never reused after deletion. Tombstones remain in history/export and prevent reuse; hard purge is admin-only outside MVP, and any future purge must retain a non-reuse registry or equivalent invariant. Export-format version is distinct from database schema revision. Unknown versions are rejected. A future migration requires a reviewed pre-migration backup, migration fixture and rollback procedure; no such test was executed here. Backup creation is separate from restore verification. A future restore test must import into an isolated instance, compare counts/references/permissions and replay cursors, and demonstrate that credentials/grants were not leaked. Those are planned checks, not evidence of success.

## 7. Contract examples and document checks

UUID examples below express shape only, not a selected generator. Every example is checked against the declared required fields, ID types, tenant scope and error definitions in sections 2, 3 and 5.

Valid WH-API-03 Signature update (authenticated editor; actor and audit fields supplied by the server):

    {"mapId":"00000000-0000-4000-8000-000000000421","requestId":"00000000-0000-4000-8000-000000000501","entityType":"Signature","entityId":"00000000-0000-4000-8000-000000000111","expectedRevision":7,"idempotencyKey":"signature-edit-501","patch":{"group":"Wormhole","type":"Unstable Wormhole"}}

Success envelope: ok=true, revision=8, committed event {eventId, mapId, sequenceNo, entityId, revision:8, eventType:"signature.updated", payload, actorId, occurredAt}. Required fields present: mapId, requestId, entityType, entityId, expectedRevision, idempotencyKey, patch; patch touches only mutable group/type.

Invalid: rebinding a signature to another system — patch {"systemId":"00000000-0000-4000-8000-000000000302"} returns E_INVALID_PAYLOAD only, because Signature.systemId is declared immutable in section 3.

Invalid revision mismatch response (E_CONCURRENT_REVISION; only the authorized current entity is returned):

    {"ok":false,"revision":8,"entity":{"signatureId":"00000000-0000-4000-8000-000000000111","systemId":"00000000-0000-4000-8000-000000000301","name":"WAM-436","group":"Wormhole","type":"Unstable Wormhole","revision":8},"errors":[{"code":"E_CONCURRENT_REVISION","message":"expected revision 7, current revision 8","field":"expectedRevision"}]}

Invalid cross-map binding (E_CROSS_MAP after target-map authorization):

    {"ok":false,"errors":[{"code":"E_CROSS_MAP","message":"signature 000...111 belongs to map 000...421, not the addressed map","field":"entityId"}]}

Invalid WH-API-02 JumpEvidence create with negative mass:

    {"mapId":"00000000-0000-4000-8000-000000000421","requestId":"00000000-0000-4000-8000-000000000502","entityType":"JumpEvidence","connectionId":"00000000-0000-4000-8000-000000000201","characterActorId":"00000000-0000-4000-8000-000000000101","jumpDate":"2026-11-02T07:00:00Z","source":"manual observed jump","shipMass":-250000000,"idempotencyKey":"jump-evidence-create-00000000-0000-4000-8000-000000000502"}

Response:

    {"ok":false,"errors":[{"code":"E_INVALID_PAYLOAD","message":"shipMass must be >= 0","field":"shipMass"}]}

Invalid future timestamp on JumpEvidence (jumpDate beyond clock tolerance) returns E_INVALID_PAYLOAD only; no game-constant mass verdict is emitted. Missing source or an unauthorized/lacking-consent actor likewise returns E_INVALID_PAYLOAD or E_FORBIDDEN; E_FORBIDDEN is used only when the actor lacks consent or authorization to share the jump on that map.

## 8. Source trace and residual prerequisites

All citations refer to the immutable commits and exact paths listed in section 1, with inline line ranges: Pathfinder ConnectionModel.php lines 1-160 (of 647) informs connection field examples (source/target same system; jump mass buckets S/M/L/Xl as inspected upstream examples only, not adopted policy); SystemSignatureModel.php lines 1-160 (of 364) inform signature-to-system/connection relationships and set_connectionId same-system validation; MapModel.php lines 1-160 (of 1579) inform map settings (active default 1, allowUnknownSystems default 0). WHMapperContext.cs lines 1-104 shows map-scoped relationships and indexes, not proof of authorization enforcement. WHMapAccess.cs lines 1-48 documents an empty-list permissive policy; this new contract deliberately proposes explicit grants, pending owner review rather than silently adopting that upstream default. WHSignature.cs lines 1-113 and WHSignatureHelperImportTests.cs lines 1-115 inform signature comparison (null type equals empty type) and parser fixtures (only 100% signal variants count as fully scanned). WHSystemLink.cs lines 1-49 and WHJumpLog.cs lines 1-47 inform connection/jump records; they do not establish a live ESI jump-log endpoint. README deployment/authentication claims and licence notices remain documentation evidence only.

Residual prerequisites: owner selection of stack and permission defaults; authoritative identity/location API capabilities, consent, scopes, rate limits and data/game rules; schema generator and timestamp/clock policies; export/cache/history retention; deployment sizing and restore/migration tests; full dependency/asset/game-data licence and security review. Integration with route/UI/security parts remains a later assembly proposal. Numeric defaults are not silently accepted. This draft is not accepted, merged, implemented or certified build-ready.
