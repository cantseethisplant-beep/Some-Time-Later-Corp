# WH BLUEPRINT CANDIDATE — NOT ACCEPTED

**Task:** MAP-042 — Corrected WH blueprint and builder handoff  
**Claim worker:** hermes-laptop-map-042-auto-20261030  
**Claim commit:** 5352b3a4d910ef1e373fe839f90f96ecdd521414  
**Input revision:** 849978908daabe3d2a45f0e758625eedc4bdde30  
**Output path:** docs/map/specs/loop-map-042-wh-design.md  
**Status:** draft candidate for review — not accepted, not merged, not build-ready, no implementation claimed  
**WH version:** 1, WH stage: 7, loop policy: 1, loop kind: wh-design

---

## 1. Purpose and evidence limits

This document is the MAP-042 deliverable: the corrected WH-first blueprint candidate assembled from the four completed, unaccepted design parts MAP-036 through MAP-039, reconciled against the targeted audit findings in MAP-041, and grounded in the pinned owner brief and inspected upstream extracts.

It is a planning record only. No requirement is accepted, no stack is selected, no code is implemented, no test is executed, and nothing is deployed. Cloud hosting remains an optional module behind a clean boundary and is not a mapper MVP prerequisite. All sources are labelled with their actual evidence status. Missing owner decisions, upstream identity/version/licence verification, compatibility/resource/restore evidence, and access remain precise prerequisites — none are repaired by invention.

Evidence is limited to the pinned immutable inputs at revision 849978908daabe3d2a45f0e758625eedc4bdde30:

- docs/map/WH-FIRST-BRIEF.md — owner WH-first direction; complete pinned file.
- docs/map/research/pf-sources.md — Pathfinder commit 06af7d86fe6456947fb960220c54d02a8623c0ff: LICENSE lines 1-22; README.md lines 1-61; composer.json lines 1-81; app/Model/Pathfinder/ConnectionModel.php lines 1-160 of 647; app/Model/Pathfinder/SystemSignatureModel.php lines 1-160 of 364; app/Model/Pathfinder/MapModel.php lines 1-160 of 1579.
- docs/map/research/wh-sources.md — EVE-WHMapper commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: LICENSE lines 1-22; README.md lines 1-60; src/WHMapper/WHMapper.csproj lines 1-52; Models/Db/WHSignature.cs lines 1-113 of 113; Models/Db/WHMapAccess.cs lines 1-48 of 48; Data/WHMapperContext.cs lines 1-104 of 104; deploy/docker/eve-whmapper/docker-compose.yml lines 1-46; Models/Db/WHSystemLink.cs lines 1-49 of 49; Models/Db/WHJumpLog.cs lines 1-47 of 47; Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1-43 of 43; src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115 of 115.

All four source drafts and MAP-041 are completed unaccepted designs for synthesis/audit only — not accepted requirements, not dependency satisfaction, not verified technical evidence. Citations reference repository commit/path/line ranges; anything uncited is proposed design or audit opinion, not upstream fact.

---

## 2. Source inventory and ID crosswalk

The four source drafts use independent local IDs. The canonical MAP-042 scheme below is the reconciliation authority; it does not claim the drafts already agreed. Findings keep their original MAP-041 IDs WH-F01..WH-F16 throughout this document; the crosswalk table lists them for traceability only.

| Source task | Revision | Local ID scheme | Canonical MAP-042 IDs |
|---|---|---|---|
| MAP-036 | abedc17bddc7f573f434f4dad78969471b9f3c9e | WH-R01..WH-R10 requirements | WH-042-R01..WH-042-R10 |
| MAP-037 | fb2bb57a8f28f5362912f6c4a94d5845dbaabd2a | WH-D / WH-API domains; WH-API-01..WH-API-16 operations | WH-042-D / WH-042-API domains; WH-042-API-01..WH-042-API-16 operations |
| MAP-038 | d68d560c9f6687f96bf82de8a980b13c385a7f2b | WH-SEC01..WH-SEC08 misuse cases | WH-042-SEC01..WH-042-SEC08 |
| MAP-039 | 556f3f983f9b1d3b2b3acc20853bcfd18c797348 | WH-B01..WH-B07 build steps; WH-T01..WH-T11 checks | WH-042-B01..WH-042-B07; WH-042-T01..WH-042-T11 |
| MAP-040 | 3b106a956ed936af87f80ffcc293741ebf9303bc | Assembled pre-audit candidate | Historical synthesis input, superseded for navigation by this corrected candidate; not independently accepted |
| MAP-041 | fa913fc258b0b459e57499220ef31476a6f392bc | WH-F01..WH-F16 audit findings | WH-F01..WH-F16 (retained unchanged; traceable below) |

Canonical MAP-042 identifiers are defined by this crosswalk. Legacy WH-D/WH-API labels retained in explanatory text resolve through the same crosswalk; the detailed component documents use their original local IDs. Source facts cite commit/path/line ranges; proposed schema rules are labelled as such.

---

## 3. Reuse decision and alternatives (proposed)

MAP-036 compared Pathfinder (PHP 8.5 per README badge; composer.json requires php-64bit >=8.2, Fat Free Framework 3.9.*, ext-pdo, ext-openssl, ext-curl, ext-json, ext-mbstring, ext-ctype, ext-gd, ext-sodium) with EVE-WHMapper (C# net10.0, EF Core 10.*, PostgreSQL via Npgsql, MudBlazor, SignalR.Client, Serilog, OpenTelemetry). Runtimes and dependency graphs are incompatible; PHP and C# internals must not be combined by assertion, and forking either imports a whole unselected stack.

**Proposed decision, not owner-selected:** new implementation informed by both, copying no substantial source. Borrow structural patterns only:

- Link plus jump-log evidence (EVE-WHMapper WHSystemLink/WHJumpLog).
- Signature dedupe/probe-complete (WHSignature HasSameContent/IsIdentified and import tests).
- Per-map access entries (WHMapAccess).
- ESI SSO/PKCE and encrypted-token-at-rest pattern (Pathfinder README).
- Map isolation (both).

Retain the upstream copyright and permission notices when copying software or substantial portions under the reproduced MIT licences. This design references patterns; any later source copying requires recording the exact files and applicable notices.

**Alternatives:** (a) fork Pathfinder if owner selects PHP; (b) fork EVE-WHMapper if owner selects .NET. Both require separate dependency, asset and game-data licence checks plus a stack commitment that does not exist. Licence inventory status: both root licences MIT (Pathfinder 2017 Mark Friedrich; EVE-WHMapper 2023 pfh59). Transitive dependencies, assets (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json) and EVE game data/ESI terms are unverified and out of scope.

---

## 4. Licensing/provenance register

| Source | Commit | Extracted files (pinned paths) | Copyright holder | Licence | Notice obligation | Substantial copy in this design? | Unverified items |
|---|---|---|---|---|---|---|---|
| Pathfinder | 06af7d86fe6456947fb960220c54d02a8623c0ff | docs/map/research/pf-sources.md: LICENSE lines 1-22; README.md lines 1-61; composer.json lines 1-81; app/Model/Pathfinder/ConnectionModel.php lines 1-160 of 647; app/Model/Pathfinder/SystemSignatureModel.php lines 1-160 of 364; app/Model/Pathfinder/MapModel.php lines 1-160 of 1579 | Mark Friedrich (2017) | MIT | Copyright and permission notice included in all copies or substantial portions | None; structural/pattern reference only | Transitive composer dependencies; assets (favicon/logo); EVE game data/ESI terms; database/runtime specifics not named in extract |
| EVE-WHMapper | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | docs/map/research/wh-sources.md: LICENSE lines 1-22; README.md lines 1-60; src/WHMapper/WHMapper.csproj lines 1-52; Models/Db/WHSignature.cs lines 1-113 of 113; Models/Db/WHMapAccess.cs lines 1-48 of 48; Data/WHMapperContext.cs lines 1-104 of 104; deploy/docker/eve-whmapper/docker-compose.yml lines 1-46; Models/Db/WHSystemLink.cs lines 1-49 of 49; Models/Db/WHJumpLog.cs lines 1-47 of 47; Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1-43 of 43; src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115 of 115 | pfh59 (2023) | MIT | Copyright and permission notice included in all copies or substantial portions | None; structural/pattern reference only | Transitive NuGet packages; embedded asset wh-effects.json; Docker images; EVE game data/ESI terms |

Both inspected roots are MIT; no root-licence conflict is established between them. The reproduced MIT notice applies to copies of the software or substantial portions; dependencies/assets/data may carry separate terms. Dependencies, assets and EVE game data/ESI terms require separate checks before any copying; no dependency compatibility, vulnerability, or licence-conflict conclusion is drawn here.

---

## 5. Requirements (WH-first MVP, proposed)

Restated from MAP-036 WH-R01..R10 with origin/source, inputs, outputs and acceptance. All proposed; none accepted. Source citations use commit/path/line ranges.

### WH-042-R01 Shared chain map
- **Origin:** owner brief proposed scope. **Source:** Pathfinder MapModel/ConnectionModel (pf-sources MapModel.php lines 1-160 of 1579; ConnectionModel.php lines 1-160 of 647); EVE-WHMapper WHMaps/WHSystems/WHSystemLinks (wh-sources WHMapperContext.cs lines 1-104; WHSystemLink.cs lines 1-49).
- **Inputs:** system identity, connection endpoints, map scope.
- **Outputs:** persisted map with systems and directional links; per-map isolation.
- **Acceptance:** a map contains systems and links; links reference exactly two systems in the same map; no system or link leaks between maps without an explicit access grant.

### WH-042-R02 Signature paste/import/edit/history
- **Origin:** owner brief proposed scope. **Source:** EVE-WHMapper WHSignature.cs lines 1-113; import tests lines 1-115; Pathfinder SystemSignatureModel.php lines 1-160 of 364.
- **Inputs:** raw scan text, system id, observer id, timestamp, signal strength.
- **Outputs:** signature record with unresolved/resolved group, optional wormhole type, created/updated audit fields, change history.
- **Acceptance:** unchanged scan import reports no change; resolved-group change counts one fully-scanned creation/change; partial-signal resolution does not count as fully scanned; duplicate active (mapId, systemId, name) is detected; group/type are mutable content, not an alternative identity key.
- **Note:** signature name max-length (upstream 7 chars per WHSignature.cs [StringLength(7)]) is referenced as upstream evidence only and is declared undecided for this candidate (OD-11 (§15 item 11)).

### WH-042-R03 Timestamps and stale observations
- **Origin:** owner brief (source/time/uncertainty retention). **Source:** Pathfinder created/updated/eolUpdated (ConnectionModel.php lines 1-160); EVE-WHMapper Created/Updated/JumpDate (WHSignature.cs lines 1-113; WHJumpLog.cs lines 1-47).
- **Inputs:** observation event with observed-at time and source.
- **Outputs:** stored observation with observed-at, source id, stale-after policy, staleness flag.
- **Acceptance:** every observation carries observed-at time and source; observations older than the proposed stale threshold are marked stale (threshold TBD by owner; proposed placeholder, not a mandate).

### WH-042-R04 Hole life/size/mass and jump evidence
- **Origin:** owner brief. **Source:** Pathfinder ConnectionModel nominalLifespan, EOL-related fields, JUMP_MASS_TYPES/JUMP_MASS_BUCKETS constants (ConnectionModel.php lines 1-160; inspected upstream examples only, not adopted policy); EVE-WHMapper WHSystemLink EndOfLifeStatus/Size/MassStatus (WHSystemLink.cs lines 1-49); WHJumpLog ship mass/character/jump date (WHJumpLog.cs lines 1-47).
- **Inputs:** observed connection attributes, jump events with pilot/ship/mass.
- **Outputs:** connection record with life/size/mass status and linked jump-log entries.
- **Acceptance:** each connection stores observed EOL status, size class, mass status; jump log links pilot character, ship type/item, mass estimate, jump date; mass estimates are labelled estimates, never exact remaining mass.

### WH-042-R05 Route planning over mapped connections
- **Origin:** owner brief. **Source:** Pathfinder Route reference (ConnectionModel.php import); EVE-WHMapper Route Planner Module over stargates and mapped wormholes (README lines 1-60).
- **Inputs:** origin system, destination system, map scope, jump-capable ship constraints (proposed).
- **Outputs:** ordered route with stargate and wormhole hops.
- **Acceptance:** route uses only mapped connections within scope plus known stargate edges; route output is a plan, not a guaranteed safe route; no hostile-detection promise.

### WH-042-R06 Per-map permissions
- **Origin:** owner brief. **Source:** EVE-WHMapper WHMapAccess.cs lines 1-48 (empty list = all instance members; entries = explicit grants only); Pathfinder map settings/activity log (MapModel.php lines 1-160).
- **Inputs:** map id, eve entity id, grant action.
- **Outputs:** access-control decision per map.
- **Acceptance:** explicit-grant-only is the candidate default; permissive empty-list behavior is an optional owner override, not adopted by default; no tenant leakage between maps in the same instance. Explicit-grant-only remains a proposed default pending owner decision (OD-13 (§15 item 13)).

### WH-042-R07 Opt-in pilot/location tracking
- **Origin:** owner brief (opt-in). **Source:** EVE-WHMapper README tracking claims (README lines 1-60 — README claim, not verified behavior).
- **Inputs:** user opt-in consent, ESI token, character id.
- **Outputs:** current-location observation tied to consented character.
- **Acceptance:** tracking only for opted-in characters; consent revocable; no location data stored without opt-in; no live ESI access claimed here. Default opt-in state, sharing expiry, and per-jump vs continuous are unresolved owner decisions (OD-14 (§15 item 14)).

### WH-042-R08 Basic notes and observed intel
- **Origin:** owner brief. **Source:** EVE-WHMapper WHNote (WHMapperContext.cs lines 1-104); Pathfinder map/system description fields (MapModel.php lines 1-160).
- **Inputs:** map id, optional system id, note text, author, timestamp.
- **Outputs:** intel note attached to map/system.
- **Acceptance:** notes are tied to a map and optionally a system; author and timestamp retained; notes are user intel, not verified hostile detection.

### WH-042-R09 Corporation administration
- **Origin:** owner brief. **Source:** EVE-WHMapper instance admin/access tables (WHMapperContext.cs lines 1-104); Pathfinder character/map scope model (MapModel.php lines 1-160).
- **Inputs:** corporation/alliance identity, admin character, membership action.
- **Outputs:** admin and membership records; instance scoping.
- **Acceptance:** at least one admin per instance; admin can manage map access and members; non-admin cannot alter another tenant's maps.

### WH-042-R10 Backup/export/import and release recovery
- **Origin:** owner brief. **Source:** Pathfinder README backup/migration guidance (external pathfinder-containers repo, not in extract); EVE-WHMapper docker-compose Postgres data volume (wh-sources docker-compose.yml lines 1-46; no Redis volume evidenced in the extract).
- **Inputs:** map/instance data export request, import file, restore request.
- **Outputs:** export bundle, import result, recovery point.
- **Acceptance:** export produces a self-describing bundle; import validates before applying; backup creation and restore verification are distinct — a backup is not verified until a restore test passes; no restore-test evidence exists yet.

---

## 6. Schema/example/type/ID consistency checks

The following examples are restated from MAP-037 section 7 and checked at document level against the proposed fields. Pass/conditional pass below means specification consistency only, never a passing app test:

1. **Valid Signature update** (authenticated editor; actor and audit fields supplied by server):
   `{"mapId":"00000000-0000-4000-8000-000000000421","requestId":"00000000-0000-4000-8000-000000000501","entityType":"Signature","entityId":"00000000-0000-4000-8000-000000000111","expectedRevision":7,"idempotencyKey":"signature-edit-501","patch":{"group":"Wormhole","type":"Unstable Wormhole"}}`
   - Required fields present: mapId, requestId, entityType, entityId, expectedRevision, idempotencyKey, patch.
   - Patch touches only mutable group/type; systemId absent so immutable rebinding is not triggered.
   - **Pass** against declared fields/types.

2. **E_CONCURRENT_REVISION response:**
   `{"ok":false,"revision":8,"entity":{"signatureId":"00000000-0000-4000-8000-000000000111","systemId":"00000000-0000-4000-8000-000000000301","name":"WAM-436","group":"Wormhole","type":"Unstable Wormhole","revision":8},"errors":[{"code":"E_CONCURRENT_REVISION","message":"expected revision 7, current revision 8","field":"expectedRevision"}]}`
   - Passes envelope contract; only authorized current entity returned.

3. **E_CROSS_MAP response:**
   `{"ok":false,"errors":[{"code":"E_CROSS_MAP","message":"signature ... belongs to map ...421, not the addressed map","field":"entityId"}]}`
   - Passes; E_CROSS_MAP used only after target-map authorization.

4. **Negative shipMass (WH-API-02):**
   `{"mapId":"00000000-0000-4000-8000-000000000421","requestId":"00000000-0000-4000-8000-000000000502","entityType":"JumpEvidence","connectionId":"00000000-0000-4000-8000-000000000201","characterActorId":"00000000-0000-4000-8000-000000000101","jumpDate":"2026-11-02T07:00:00Z","source":"manual observed jump","shipMass":-250000000,"idempotencyKey":"jump-evidence-create-00000000-0000-4000-8000-000000000502"}`
   - Returns `{"ok":false,"errors":[{"code":"E_INVALID_PAYLOAD","message":"shipMass must be >= 0","field":"shipMass"}]}`.
   - **Conditional pass** (MAP-041 WH-F10): passes only if JumpEvidence.shipMass is declared `number >= 0` in the candidate schema; restated here as proposed.

These are document checks of proposed contracts, not observed server responses. All JSON identifier fields now use complete canonical UUID strings.

ID format: UUID canonical text used consistently across examples; no `whd-` prefix serialized; IDs never reused per tombstone rule. Tombstones remain in history/export; no ID-reuse examples appear. The proposed implementation must enforce cross-map isolation and return E_CROSS_MAP only after authorization. Authorization failure never reveals entity content beyond an already-addressed entity.

---

## 7. Proposed schema rules (WH-D domain)

Map-owned records inherit required mapId (System, Connection, Signature, Observation, JumpEvidence, Note and Grant); each foreign key resolves within that map. Instance is the tenant root, Map belongs to instanceId, and Actor belongs to instanceId rather than one map. Grant/Consent validate their actor and map belong to the same instance. Instance/Map/Actor records therefore do not inherit a parent mapId. Consent.targetMapId is required for map scope and null for instance scope; reads check both map authorization and applicable actor consent.

All entities use UUID text identifiers, server-set revision integer >= 1, createdAt/updatedAt UTC timestamps, createdBy/updatedBy actor UUIDs, and active boolean default true. IDs are never reused after deletion; tombstones remain in history/export.

| Entity | Key fields and invariants (in addition to common fields) |
|---|---|
| Instance | instanceId UUID PK; name required; ownerActorId UUID required; tenant root, no mapId. |
| Map | mapId UUID PK; instanceId UUID required; name required, unique within instance; no parent mapId. |
| Actor | actorId UUID PK; instanceId UUID required; eveCharacterId integer optional; displayName required; locationSharingOptIn boolean default false (proposed consent field). |
| Consent (proposed) | consentId UUID PK; actorId UUID same instance; scope enum map/instance; targetMapId optional, same map when scope=map; optIn boolean default false; grantedAt/updatedAt server-set; unique(actorId,scope,targetMapId). |
| Grant | grantId UUID PK; instanceId/mapId/actorId UUID required; role enum viewer/editor/mapAdmin; unique(mapId,actorId); cannot revoke last administrator without explicit owner transfer. |
| System | systemId UUID PK; eveSystemId integer optional; name required; classLabel optional; unique(mapId,eveSystemId) when known. |
| Connection | connectionId UUID PK; sourceSystemId/targetSystemId UUID required, distinct, same map, immutable post-create; holeType/sizeLabel/massStatus/lifeStatus optional; statusObservedAt/statusSource optional; nominalLifespan integer optional >= 0, unit/authority unresolved. |
| Signature | signatureId UUID PK; systemId UUID required same map, immutable post-create; connectionId optional, connection must have that system as endpoint; supersedesSignatureId optional, references Signature tombstone on same map, never self-references; name required; group/type/signalText optional; fullyScanned boolean required computed from parser policy; unique active(mapId,systemId,name). |
| Observation | observationId UUID PK; systemId/connectionId optional, exactly one set, same map; observedAt UTC required; source required; uncertainty optional; expiresAt UTC optional > observedAt. |
| JumpEvidence | jumpId UUID PK; connectionId UUID required same map; characterActorId UUID required within instance and authorized/consented; jumpDate UTC required; source required; uncertainty optional; shipTypeId/shipItemId integer optional; shipMass number optional >= 0, estimate only. |
| Note | noteId UUID PK; systemId optional same map; content required; no unique(mapId,systemId) constraint. |

**Duplicate signatures, reappearance, conflicting scans:** identity key is map/system/signature name; group/type are mutable content, never a second identity key. Identical imports are no-ops (no revision increment); conflicting content is returned for explicit review. Concurrent creates yield one active row enforced transactionally, E_DUPLICATE_SIGNATURE on the other. Reappearance creates a new signature ID linked by supersedesSignatureId to the old tombstone, never reviving/reusing a deleted ID.

**WH-API logical operations** (proposed, not routes; server derives actor from validated session; each request contains target mapId or instanceId, requestId UUID, idempotencyKey on mutations, expectedRevision for existing entities):

| Op | Actor | Input | Result / failure |
|---|---|---|---|
| WH-042-API-01 ReadMap | viewer | mapId, optional entity filters | authorized active entities + revision/cursor; E_FORBIDDEN/E_NOT_FOUND without other-map data |
| WH-042-API-02 CreateEntity | editor | mapId, entityType, fields | entity, revision=1, event; E_INVALID_PAYLOAD/E_CROSS_MAP/E_DUPLICATE_SIGNATURE |
| WH-042-API-03 UpdateEntity | editor | mapId, entityType, entityId, expectedRevision, patch | updated entity/revision/event; E_CONCURRENT_REVISION with authorized current entity |
| WH-042-API-04 DeleteEntity | editor | mapId, entityType, entityId, expectedRevision | tombstone/event; dependent active references fail E_REFERENCED_ENTITY |
| WH-042-API-05 PreviewScan | editor | mapId, systemId, scanText | normalized rows, previewHash, proposed changes/conflicts; no mutation |
| WH-042-API-06 CommitScan | editor | mapId, systemId, previewHash, normalized rows, expected revisions | counts, committed entities/events; transactional checks; E_CONFLICTING_SCAN |
| WH-042-API-07 PullEvents | viewer | mapId, lastSequenceNo | ordered authorized events + new cursor; E_CURSOR_EXPIRED/E_INVALID_CURSOR |
| WH-042-API-08 PushMutations | editor | mapId, mutation list with IDs, expected revisions, idempotency keys | per-mutation results, sequence numbers, cursor |
| WH-042-API-09 ExportMap | mapAdmin | mapId | versioned authorized export excluding credentials; E_FORBIDDEN |
| WH-042-API-10 ValidateImport | mapAdmin | mapId, export envelope | schema/ownership/conflict report, preview hash; no mutation |
| WH-042-API-11 CommitImport | mapAdmin | mapId, validated hash, target revision | all-or-nothing import with identity remapping |
| WH-042-API-12 ManageGrant | mapAdmin | mapId, targetActorId, role/revoke, expected grant revision | revised grant/event; cannot revoke last admin without owner transfer |
| WH-042-API-13..16 | instance admin/bootstrap | instance creation, actor registration, ownership transfer | Out of core MVP boundary; bootstrap actor is unresolved owner decision |

Every mutation atomically commits entity revision and event `{eventId, mapId, sequenceNo, entityId, revision, eventType, payload, actorId, occurredAt}`. Authorization is checked before revealing content, before idempotency lookup, and transactionally before applying writes; E_FORBIDDEN never reveals entity existence.

---

## 8. UI/workflows (proposed)

1. **Scanner paste/preview/diff/save:** paste tab-separated scan rows; preview resolves each row against existing signatures (unchanged/new/changed/below-full-strength observed-not-created); diff shows Created/Updated/CreatedBy/UpdatedBy; save persists actor, time, source-text hash, signal-strength note; unresolved rows stay "Unknow" until probed. Mirrors import-test fixtures (100% vs 42.5% signal, decimal separators — upstream fixtures only, not adopted parsing policy).
2. **Manual chain editing:** add systems, link two selected systems, edit links, lock systems against accidental moves; every edit writes an activity-log entry; duplicate system names per map rejected.
3. **Stale signatures:** hidden from route planning unless user explicitly accepts stale data; never supports a safety claim; stale flags are observations, not removals.
4. **Route selection:** filter excludes stale/unknown-mass/denied-access links; ranks fewest hops then fewest wormholes; displays per-leg uncertainty; explicit acceptance before sharing.
5. **Notes/intel:** attach to map plus optional system; source/time/uncertainty retained; observed events only.
6. **Offline/denied/empty:** offline edits may queue locally as uncommitted proposals and must reauthorize/revalidate revisions on reconnect; write failures fail fast with user-visible message; denial returns a non-leaking generic reason; empty map shows first-system prompts; no credentials or raw debug logs persisted/displayed.

---

## 9. Dependency-ordered build milestones (proposed)

The IDs retain their source crosswalk, but the execution order below is deliberately B00 → B01 → B05 → B02/B03/B04 → B06 → B07. Independent feature work may proceed only after its listed prerequisites. Until the identity/bootstrap/permission decisions are resolved, use isolated synthetic fixtures and a deny-by-default test actor; no live tokens, player data or public deployment. B05 is a shared gate for every real read/write/event, not security postponed until after feature release.

| Milestone | Prerequisites / inputs | Outputs | Observable future checks |
|---|---|---|---|
| WH-042-B00 Freeze build baseline | OD-02 stack choice; OD-10 bootstrap; owner review of OD-13/14 permission/consent defaults | recorded decisions, selected component versions, initial-owner/tenant contract, isolated fixture plan; no deployment | reviewer can identify chosen versus unresolved decisions; unresolved choices block affected real-data milestones |
| WH-042-B01 Schema and isolated harness | B00 for selected-stack work; pinned entity contracts | typed schema/migrations, same-map FK/revision/tombstone rules, synthetic actors/maps and deny-by-default authorization interface | T02/T12/T13/T14 fixtures and schema/type checks; no real credentials |
| WH-042-B05 Identity, access, consent and notes | B01; resolved bootstrap and applicable identity/API/consent decisions | server-derived identity, grants, consent, protected reads/writes/events/cache, notes | T04/T15/T16/T17 and SEC01..08, including cross-map denial and revocation; passing source lint is insufficient |
| WH-042-B02 Scanner paste/preview/diff/save | B01, B05; pinned import fixtures | import UI/parser, preview hash, duplicate/conflict transaction | T01/T02/T11, both decimal formats and partial-signal fixtures; changed content requires revision check |
| WH-042-B03 Manual chain editing | B01, B05 | add/link/edit/lock flows and activity events | T12; duplicate system/connection policy explicit; lock behavior and cross-map FK denial consistent |
| WH-042-B04 Route planner | B01, B03, B05; authoritative graph/data inputs and OD-06 uncertainty policy | route result over permitted stargate/mapped links with provenance and uncertainty | T03/T13/T14; stale/unknown data cannot silently become a safe route |
| WH-042-B06 Import/export/migration | B01-B05; export version and identity mappings | validate/commit import, versioned export, backup/rollback scripts and isolated restore procedure | T05/T06/T08/T09; actual roundtrip, migration rollback and restore evidence remain required |
| WH-042-B07 Offline/denied/outage | all prior | local draft queue, reauthorization/revision-aware reconnect, protected cached reads | T10/T11/T15; server writes rejected offline, local edits remain uncommitted proposals; replay cannot restore revoked access |


Backup creation and restore verification are distinct; B06 covers scripts only — no restore test has been executed.

---

## 10. Test/evidence matrix

| ID | Kind | What it checks | Pinned source | Status |
|---|---|---|---|---|
| WH-042-T01 | Specification review; future runtime fixture | import fixture: unchanged → no change; empty repo → only 100% row counts; partial 42.5% → resolved but not fully scanned | import tests lines 1-115 | Proposed static check |
| WH-042-T02 | Specification review; future runtime fixture | duplicate signature name per system rejected | WHMapperContext unique index {WHId, Name} | Proposed |
| WH-042-T03 | Specification review; future runtime fixture | route excludes stale link; unknown-mass link never "safe" | MAP-039 section 3.5 | Proposed |
| WH-042-T04 | Specification review; future runtime fixture | per-map access denial for non-granted entity when entries exist | WHMapAccess.cs lines 1-48 | Proposed |
| WH-042-T05 | Specification review; future runtime fixture | export/re-import preserves timestamps, uncertainty, actor | export envelope v1 proposal | Proposed |
| WH-042-T06 | Specification review; future runtime fixture | migration script has paired rollback restoring pre-migration schema | MAP-039 B06/T06 | Proposed |
| WH-042-T07 | Specification review; future runtime fixture | MIT header on files deriving from upstream structure | pf/wh LICENSE lines 1-22 | Proposed; dependency/asset/game-data review open |
| WH-042-T08..T11 | Runtime-only | import/export roundtrip byte-level; backup checksum vs test restore into empty DB; outage read-only/write-reject/queue drain; concurrent conflict shows both versions | Future app | Not executed; require built app |


Additional proposed checks introduced during final coordination (not source claims or executed tests):

| ID | Fixture/input | Expected future result |
|---|---|---|
| WH-042-T12 | Two fixture maps, same-system and cross-map links, duplicate IDs and a locked node | permitted chain edits commit one revision/event; wrong-map FK and prohibited locked edit fail without altering either map |
| WH-042-T13 | Observation before/after a configured expiry, stale graph edge, offline cached view | data becomes explicitly stale, remains auditable, and is excluded/acknowledged under the documented route policy; no implied collapse or safety claim |
| WH-042-T14 | Jump evidence with missing source, unknown mass, negative mass and uncertain lifetime | missing/invalid fields rejected; unknown/estimated values retained as such; no exact remaining-mass or invented ESI jump feed |
| WH-042-T15 | Opt-in, authorized cached location/event, then consent/grant revocation and offline replay | no new private delivery or replay after revocation; cache invalidated; explicit reauthorization before accepting queued writes |
| WH-042-T16 | Note in map A read/exported by actor in map B; hostile markup in note | unauthorized read/export denied without content leakage; note rendered safely; provenance retained |
| WH-042-T17 | Isolated initial-owner setup, unauthorized map creation and last-admin removal | owner established only through resolved bootstrap protocol; unauthorized creation denied; last-admin removal requires explicit authorized transfer |

Requirement → build/check traceability (all proposed; the source parts retain their own local IDs):

| Requirement | Build steps | Observable checks |
|---|---|---|
| WH-042-R01 | B01, B03, B05 | T12, SEC01, SEC06 |
| WH-042-R02 | B01, B02, B05 | T01, T02, T11, SEC05 |
| WH-042-R03 | B01, B04, B07 | T03, T13 |
| WH-042-R04 | B01, B03, B04 | T14 |
| WH-042-R05 | B03, B04, B05 | T03, T13, T14 |
| WH-042-R06 | B01, B05 | T04, T12, T15, SEC01, SEC02, SEC06, SEC07 |
| WH-042-R07 | B05, B07 | T15, SEC03, SEC04 |
| WH-042-R08 | B05 | T16, SEC08 |
| WH-042-R09 | B00, B05 | T17, SEC02, SEC07, SEC08 |
| WH-042-R10 | B06, B07 | T05, T06, T08, T09, T10, SEC08 |

In this table B/T/SEC abbreviations resolve to WH-042-B/T/SEC identifiers. SEC01..08 resolve through the MAP-038 crosswalk and pinned component document section 17. SEC05's old seven-character input is an upstream fixture, not an adopted signature-length policy: final validation must follow OD-11. SEC03 must verify both upstream revocation behavior and local session/cache invalidation; a revoked external token does not by itself prove local logout. No requirement is treated as satisfied by merely writing its test specification.

A backup artefact with checksum is not recovery evidence; a tested restore into an empty database with row-count match is required and remains pending.

---

## 11. Fork/integration decision (proposed, not owner-selected)

**Options:**
- **(A) New implementation informed by both** (recommended proposal): define WH-first schema/services from the brief, borrowing structural patterns without copying substantial source. Preserve applicable MIT notices for later copies of software or substantial portions.
- **(B) Fork Pathfinder** if owner selects PHP: carries PHP 8.x/Fat Free Framework stack, composer dependencies, encrypted token-at-rest pattern; requires full dependency/asset/game-data licence checks.
- **(C) Fork EVE-WHMapper** if owner selects .NET: carries net10.0/EF Core/PostgreSQL/MudBlazor stack, NuGet dependencies; requires full dependency/asset/game-data licence checks.

**Tradeoffs:** PHP and C# internals cannot be merged by assertion; forking either imports a whole unselected stack. Owner stack decision is a prerequisite (MAP-041 WH-F08). No runtime selected.

**UI/workflows:** as in section 8, all proposed.

**Security/privacy:** server-side authorization for every read/write/event; clients never trusted; opt-in location/jump sharing with revocable consent; tokens server-side only, encrypted-at-rest pattern with fail-closed if key missing (Pathfinder pattern, not adopted implementation); revocation via ESI revoke endpoint plus server-side invalidation, runtime-unverified; activity log append-only, not cascade-deleted; cache keys namespaced by instance/map, invalidated on unlink/revocation/membership change; stale membership revalidation at login and periodically (interval unresolved). Misuse cases WH-042-SEC01..SEC08 are proposed future tests.

**Operational restore/migration/release checklist (proposed, not executed):**
- Pre-migration backup required; migration fixture and rollback procedure required; none executed.
- Export envelope v1: `{format:"wh-export",version:1,sourceInstanceId,sourceMapId,entities,events,snapshotCursor,exportedAt}`; secrets excluded; import ID/remapping table required; tombstones prevent ID reuse; hard purge admin-only outside MVP.
- Restore test must import into isolated instance, compare counts/references/permissions, replay cursors, demonstrate credentials/grants not leaked — planned check, not evidence of success.
- Backup creation is distinct from restore verification; no restore-test evidence exists.

**Optional-cloud boundary:** cloud module sits behind a clean boundary; excluded from MVP acceptance; hardware offers, catalogue deployment, distributed cloud controller are not mapper prerequisites.

**Open owner decisions tracked in this section (proposed defaults are not owner approvals):** item 11 signature name max-length undecided (OD-11 (§15 item 11)); item 13 explicit-grant-only vs permissive empty-list default requires owner decision (OD-13 (§15 item 13)); item 14 opt-in default state, sharing expiry, per-jump vs continuous require owner decisions (OD-14 (§15 item 14)).

---

## 12. Audit disposition table (WH-F IDs -> changed section / residual blocker)

All 16 MAP-041 findings are disposed below. Findings corrected in this document reference the section; unresolved items remain explicit blockers.

| WH-F ID | Severity | Class | Disposition | Changed section / residual blocker |
|---|---|---|---|---|
| WH-F01 | Medium | document-fixable | Corrected | Instance/bootstrap ops moved to out-of-MVP subsection; bootstrap actor unresolved owner decision (§7 WH-042-API-13..16 note; OD-10 (§15 item 10)). |
| WH-F02 | Medium | owner | Open — owner decision | Explicit-grant-only marked proposed pending owner decision; cites WHMapAccess.cs lines 1-48 (§5 R06; OD-13 (§15 item 13)). |
| WH-F03 | Medium | document-fixable | Corrected | Name max-length declared undecided; upstream 7-char constraint cited as reference only (OD-11 (§15 item 11)). |
| WH-F04 | Medium | document-fixable | Corrected | Optimistic revision conflict adopted as single rule; last-write-wins only as explicit owner exception with audit entry (§7 WH-042-API-03 row; OD-01 (§15 item 1)). |
| WH-F05 | Low | not-a-defect | Closed | Signature per system with optional connectionId validated same-system; no cardinality contradiction (§7 schema; §6). |
| WH-F06 | High | document-fixable | Corrected | Bootstrap actor/initial owner designation recorded as unresolved; no self-bootstrapping implied (§7 WH-042-API-13..16; OD-10 (§15 item 10)). |
| WH-F07 | High | document-fixable | Corrected | B06 restated as scripts only; backup creation ≠ restore verification; no restore-test evidence; no Redis volume evidenced (§5 R10; §9; §11). |
| WH-F08 | High | owner | Open — owner decision | Stack decision prerequisite; PHP vs C# incompatibility listed as blocker; no runtime selected (§3; §11). |
| WH-F09 | High | upstream-evidence | Open — blocker | Auth/token implementation, consent workflow, revocation effectiveness, ESI scopes/rate limits marked missing evidence (§4; §11). |
| WH-F10 | Medium | document-fixable | Corrected | JumpEvidence.shipMass restated as `number >= 0`; decimal separators are upstream fixtures only (§7 schema; §6). |
| WH-F11 | Medium | owner | Open — owner decision | Opt-in default, sharing expiry, per-jump vs continuous listed as unresolved owner decisions (§5 R07; OD-14 (§15 item 14)). |
| WH-F12 | Medium | document-fixable | Corrected | Import ID/remapping table required; tombstones prevent ID reuse; re-import duplicate prevention added (§6 export/import; §11 operational checklist). |
| WH-F13 | Medium | document-fixable | Corrected | Consent model labelled proposed; ESI scopes/rate limits/issuer unknown blocker added (§5 Consent entity; §11). |
| WH-F14 | Medium | document-fixable | Corrected | JUMP_MASS_BUCKETS explicitly one implementation's constants, not adopted policy; mass-bucket mapping unresolved placeholder (§5 R04; §11). |
| WH-F15 | Medium | document-fixable | Corrected | Full dependency licence/security audit for both manifests missing; audit-ignore entry requires review (§4; §11). |
| WH-F16 | Low | document-fixable | Corrected | Database engine undecided; docker-compose optional background only; no Redis volume evidenced (§7 domain boundaries; §11). |

No ID appears in two classes; no finding was silently dropped.

---

## 13. Source-answerable corrections applied

The following corrections from MAP-041 are applied in this document:

1. **Concurrent-edit contradiction (WH-F04):** MAP-037's optimistic `expectedRevision`/`E_CONCURRENT_REVISION` and MAP-039's "last-write-wins with activity log" are reconciled by adopting optimistic revision conflict as the single rule, with last-write-wins only as an explicit owner exception requiring an audit entry (OD-01 (§15 item 1)).
2. **Instance/bootstrap ops in MVP scope (WH-F01, WH-F06):** WH-API-13..16 are explicitly out of core MVP boundary; bootstrap actor is an unresolved owner decision (OD-10 (§15 item 10)).
3. **Explicit-grant-only default presented as decided (WH-F02):** relabelled as proposed pending owner decision, citing WHMapAccess.cs lines 1-48 permissive upstream default (OD-13 (§15 item 13)).
4. **Dropped 7-char signature name limit (WH-F03):** name max-length declared undecided; upstream constraint cited as reference only (OD-11 (§15 item 11)).
5. **Restore-test evidence gap (WH-F07):** B06 restated as scripts only; backup creation vs restore verification kept distinct; no Redis volume claim (§11).
6. **Stack decision missing (WH-F08):** explicitly stated as owner prerequisite with PHP vs C# incompatibility blocker (§3; §11).
7. **Token/revocation presented as pattern (WH-F09):** libsodium pattern marked as reference only; auth/token implementation, consent workflow, revocation effectiveness listed as blockers (§4; §11).
8. **shipMass type missing (WH-F10):** restated as `number >= 0`; conditional pass on negative-mass example (§6).
9. **Opt-in default/expiry undecided (WH-F11):** listed as unresolved owner decisions (OD-14 (§15 item 14)).
10. **Tombstone/remapping not operationalized (WH-F12):** import ID/remapping table required; re-import duplicate prevention added (§11 operational checklist).
11. **Consent model without ESI scopes (WH-F13):** consent model labelled proposed; ESI scopes/rate limits/issuer blocker added (§11).
12. **Mass buckets presented ambiguously (WH-F14):** JUMP_MASS_BUCKETS explicitly one implementation's constants, not adopted policy (§5 R04; §11).
13. **Dependency audit incomplete (WH-F15):** transitive dependencies for both manifests listed as missing (§4; §11).
14. **Database implied but unnamed (WH-F16):** database engine undecided; docker-compose optional background only (§7 domain boundaries; §11).

---

## 14. Separation of checks performed vs future tests

**Historical native/coordinator checks reported in the source packet (document-level, not runtime evidence):**
- Commit/path/line citation spot-checks across all pinned extracts.
- Four MAP-037 examples checked against required fields, types, ID format, tenant scope and error definitions.
- WH-F05 cardinality check closed as not-a-defect.
- Backup creation vs restore verification distinction verified in text; no restore-test claim made.
- Docker-compose Postgres-only volume evidence verified; no Redis volume claimed.
- Both root MIT licences reproduced; notice obligation scoped to substantial copies only.

**Future runtime/compatibility tests (require the built app; not executed here):**
- Import/export roundtrip byte-level comparison (WH-042-T08).
- Backup checksum vs test restore into empty database with row-count match (WH-042-T09).
- Service outage: cached reads, write rejection, queue drain on reconnect (WH-042-T10).
- Concurrent edit conflict surfaces both versions and invalidates stale cache (WH-042-T11).
- Per-handler authorization implementation and testing (runtime).
- ESI scopes, rate limits, issuer runtime contract verification (upstream-evidence).
- Full dependency licence/security audit for composer.json and csproj (upstream-evidence).
- Asset licence check (favicon/logo; wh-effects.json); EVE game data/ESI terms-of-use (upstream-evidence).
- Restore test into isolated instance comparing counts/references/permissions and replaying cursors (operational).

---

## 15. Remaining owner/evidence decisions (precise, with affected steps)

1. **OD-01 — Concurrent-edit exception policy** — optimistic revision conflict adopted as single rule; last-write-wins only as explicit owner exception with audit entry; affects WH-042-API-03 (WH-F04).
2. **OD-02 — Target language/runtime/stack decision** (PHP Pathfinder fork vs C# EVE-WHMapper fork vs new implementation) — owner decision; blocks WH-042-B01 and all build milestones (WH-F08).
3. **OD-03 — ESI scopes, rate limits, issuer runtime contract; consent workflow evidence** — missing; blocks WH-042-B05 opt-in tracking and WH-042-API-09 export consent/visibility (WH-F09, WH-F11, WH-F13).
4. **OD-04 — Full dependency licence/security audit** for composer.json and csproj; audit-ignore entry review — missing; blocks any copying decision (WH-F15).
5. **OD-05 — Asset licence check** (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json); **EVE game data/ESI terms-of-use** — unchecked (WH-F15).
6. **OD-06 — Numeric stale threshold, mass-bucket mapping, route-constraint values** — owner placeholders; blocks WH-042-B04 route planner acceptance (WH-F14).
7. **OD-07 — Auth/token-storage implementation; encrypted-at-rest pattern not adopted; revocation effectiveness unverified** — blocks WH-042-API auth design (WH-F09).
8. **OD-08 — Restore-test evidence missing** — backup creation ≠ restore verification; blocks release recovery acceptance (WH-F07).
9. **OD-09 — Unseen handler implementations** — per-handler authorization must be implemented and tested (runtime).
10. **OD-10 — Bootstrap actor/initial owner designation mechanism** — missing; blocks WH-042-API-13..16 (WH-F06).
11. **OD-11 — Signature name max-length (7 upstream)** — undecided in candidate schema (WH-F03).
12. **OD-12 — Database engine undecided** — docker-compose Postgres is example only (WH-F16).
13. **OD-13 — Explicit-grant-only vs permissive empty-list default** — owner decision required before build acceptance (WH-F02).
14. **OD-14 — Opt-in default state, sharing expiry, per-jump vs continuous** — owner decisions (WH-F11).

These are precise prerequisites, not repaired by inventing facts. Independent acceptance, required technical evidence and a frozen revision still govern the completion gate.

---

## 16. Acceptance criteria mapping

- **Exact scoped deliverable with stable identifiers, concrete examples/checks and source-linked decisions:** sections 2, 4-12 provide canonical IDs, checked examples, and commit/path/line citations throughout.
- **WH-first scope preserved with optional cloud and exact residual blockers:** section 11 optional-cloud boundary; section 15 lists all residual blockers; cloud excluded from MVP acceptance.
- **No invented tests or approvals:** section 10 status column labels every check proposed/static or runtime-only/not executed; no acceptance, merge, deployment or build-ready certification claimed.
- **Apply every source-answerable correction:** section 13 lists all 14 applied corrections mapped to MAP-041 findings.
- **Audit disposition table WH-F IDs -> changed section and exact verification or explicit residual blocker:** section 12.
- **Check ID crosswalks, entities versus API examples, schema/permission invariants, requirement -> dependency-ordered build step -> observable test traceability, source pins and WH-first scope:** sections 2, 5-6, 9-10.
- **Provide enough concrete data fields/operations/error examples and build milestones for a later builder to start:** sections 5-9.
- **Include proposed fork/integration decision with alternatives, UI/workflows, security/privacy, operational restore/migration/release checklist and optional-cloud boundary:** section 11.
- **Separate document checks performed from future runtime/compatibility tests:** section 14.
- **List only precise remaining owner/evidence decisions with affected steps:** section 15.
- **Title: WH BLUEPRINT CANDIDATE — NOT ACCEPTED:** header and status throughout.
- **No self-acceptance or build-ready certification; stop with a review handoff:** this section and the BEGIN HANDOFF below.

This document is the complete MAP-042 output. It is a candidate for review, not acceptance, merge, deployment or certification as build-ready.


## 17. Final coordinator review and builder entry point

Read sections 15 (OD decisions), 9 (ordered build plan), 7 (contracts), 10 (checks/traceability) and 12 (audit disposition) before implementation. Detailed component drafts and the original audit remain in the accompanying package at immutable revisions. Proposed changes here reconcile those drafts; they do not rewrite source history or accept the requirements. The package is a completed planning/review candidate. It is not a frozen implementation baseline: resolve the named prerequisite decisions/evidence for the affected milestone, then record independent acceptance. No broad discovery rerun is required to locate the plan; specific upstream/runtime checks listed in OD decisions are still necessary.

The owner explicitly requested final coordinator completion. Native draft/raw/critic history is preserved. The last native critic requested reference corrections; Codex corrected those plus the documented consistency/traceability issues, without regenerating or resetting budgets. There was no fresh native critique of this corrected revision. Final packaging and JSON/reference checks are document checks only; they are not app/runtime/security/restore evidence.
