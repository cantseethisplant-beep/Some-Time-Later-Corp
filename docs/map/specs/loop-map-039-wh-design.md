# WH User Workflows, Routing Uncertainty and Operational Test Plan

MAP-039 design specification — draft, unaccepted. Owner direction: docs/map/WH-FIRST-BRIEF.md (input revision 849978908daabe3d2a45f0e758625eedc4bdde30) takes precedence; wormhole mapping/intel/operations is the core, cloud hosting is an optional module.

## 1. Scope and evidence base

This document converts the WH-first brief into a concrete design: shared system/connection chain map; probe-signature paste/import/edit/history; timestamps and stale observations; observed hole life/size/mass and jump evidence; route planning over mapped connections; per-map permissions; opt-in pilot/location tracking; basic notes and observed intel; corporation administration; backup/export/import and release recovery.

Pinned inputs (immutable extracts only; not runtime verification or a full licence/security audit):

- docs/map/WH-FIRST-BRIEF.md @ 849978908daabe3d2a45f0e758625eedc4bdde30
- docs/map/research/pf-sources.md @ 06af7d86fe6456947fb960220c54d02a8623c0ff: Pathfinder LICENSE lines 1-22, README lines 1-61, composer.json lines 1-81, app/Model/Pathfinder/ConnectionModel.php lines 1-160 of 647, SystemSignatureModel.php lines 1-160 of 364, MapModel.php lines 1-160 of 1579.
- docs/map/research/wh-sources.md @ 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: EVE-WHMapper LICENSE lines 1-22, README lines 1-60, src/WHMapper/WHMapper.csproj lines 1-52, Models/Db/WHSignature.cs lines 1-113, Models/Db/WHMapAccess.cs lines 1-48, Data/WHMapperContext.cs lines 1-104, deploy/docker/eve-whmapper/docker-compose.yml lines 1-46, Models/Db/WHSystemLink.cs lines 1-49, Models/Db/WHJumpLog.cs lines 1-47, Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1-43, src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115.

Both inspected root licences are MIT. Retain copyright and permission notices for any copied substantial material; dependencies, assets and game data require separate checks before implementation.

Citation convention: commit/path/line ranges below refer to the pinned extracts. Everything not so cited is proposed design or test plan, not accepted implementation and not upstream fact.

## 2. Baseline intent versus proposed rules

Baseline intent (owner brief plus upstream README claims; not adopted as requirements): scan import, manual chain edit, link creation (upstream describes selecting systems and pressing L), per-map access lists, pilot location tracking, route planner over stargates and wormholes, jump logs with hole size/status, optional Docker-based hosting.

Proposed rules (new; owner decision required where marked):

- Every observation carries source, observed-at time and uncertainty; observed and estimated mass/life are never exact.
- Staleness window [T_stale — owner decision; no game constant assumed]; stale holes invalidate "safe route" claims and unknown activity invalidates safety claims.
- Route filtering excludes stale/unknown-mass links unless the user explicitly acknowledges stale data.
- Concurrent-edit conflict surfaces both versions; last-write-wins only with an activity-log record.
- MIT header added to files deriving materially from Pathfinder (PHP) or EVE-WHMapper (C#) structure.

## 3. User workflows

### 3.1 Scanner paste / preview / diff / save

1. Paste raw scan text into the import box. Upstream import-test shape is tab-separated rows carrying name, group/type, subtype, signal strength and distance (wh-sources, WHSignatureHelperImportTests.cs lines 1-115, fixtures SCAN and partialScan).
2. Preview resolves each row against existing signatures on the selected system: unchanged, newly created, group/type changed, below-full-strength partial treated as observed-not-created (mirrors upstream import tests).
3. Diff shows resolved/unresolved, created/changed and audit fields Created/Updated/CreatedBy/UpdatedBy (inspected source WHSignature.cs lines 1-113).
4. Save persists actor, time, source-text hash and signal-strength note; unresolved rows stay group "Unknow" until probed (WHSignature.cs IsIdentified()).

### 3.2 Manual chain editing

Add systems, link two selected systems, edit links, lock systems against accidental moves (upstream README feature claims, wh-sources README lines 1-60). Proposed: every edit writes an activity-log entry with actor and time; locked systems require unlock before link deletion; duplicate system names per map are rejected (WHMapperContext unique index {WHMapId, Name}, lines 1-104).

### 3.3 Stale signatures

A signature is stale when its last refresh predates [T_stale]. Stale signatures are hidden from route planning unless the user explicitly accepts stale data. A stale hole must never support a safety claim; unknown activity invalidates safety claims. Stale flags are observations, not removals.

### 3.4 Jump, mass and life observations

Jump logs record link, character, date, ship type/item id and mass (WHJumpLog.cs lines 1-47). Hole size and Normal/Critical status are observation statuses (upstream README jump module), not guarantees. Observed mass and estimated remaining mass are both uncertain; the app never displays exact remaining mass. Pathfinder jump-mass buckets and lifespan thresholds appear in ConnectionModel.php lines 1-160 as inspected PHP constants; they are evidence of one implementation's shape, not adopted game constants for this app.

### 3.5 Route selection and route filtering

Route planner calculates paths over stargates and mapped wormholes for individuals or fleets (upstream README claim). Proposed filtering: exclude links with stale status, unknown mass/life, or map access denial; rank by fewest hops then fewest wormholes; display per-leg uncertainty (stale/observed/estimated); require explicit acceptance before sharing a route. No guessed game constants; any mass/lifespan numbers must be re-verified against authoritative ESI/universe data before use.

### 3.6 Notes and intel

Notes attach to map + system (WHMapperContext WHNote index {MapId, SoloarSystemId}, lines 1-104). Intel entries keep source/time/uncertainty and describe observed events only; no complete hostile-detection promise.

### 3.7 Multi-pilot conflicts

Opt-in pilot location shares location with map members; observations retain source/time/uncertainty. Concurrent edits to one connection/signature surface a conflict dialog with both versions; the actor choosing to save writes the activity log. Edit locking (upstream "lock systems") prevents accidental moves only, not concurrent logical conflicts.

### 3.8 Empty, offline, error and denied states

- Empty map: first-system/add-connection prompts, no exception.
- Offline: edits queue locally and sync on reconnect; import/export works offline.
- Error: write failures fail fast with a user-visible message; no silent data loss.
- Denied: per-map access entries govern (WHMapAccess.cs lines 1-48; when entries exist, only granted entities access); denial returns a reason; no credentials or raw debug logs are persisted or displayed.

## 4. Proposed data and permission boundaries (design only)

Cross-map isolation: systems, signatures, links, notes and routes belong to one map; deleting a map cascades its owned data (WHMapperContext cascade rules, lines 1-104). Per-map access lists control entity access; instance administration is separate (WH instance model inspected, not adopted). Reuse of the PHP Pathfinder internals or C# EVE-WHMapper internals is a proposed alternative requiring compatibility comparison; combining them by assertion is prohibited by the brief. Hosting boundary is optional and small; the Docker Compose reference (wh-sources lines 1-46) is a proposal, not a mapper prerequisite.

## 5. Operational test plan

### 5.1 Build sequence WH-B01 onwards

WH-B01 schema and repository stubs for map/system/link/signature/jump-log/note/route/access, with MIT headers where structure is reused.
WH-B02 scanner paste/preview/diff/save with fixtures.
WH-B03 manual chain editing, locks, activity log.
WH-B04 route planner with stale/unknown filtering and uncertainty display.
WH-B05 per-map access, opt-in pilot tracking, notes/intel.
WH-B06 import/export roundtrip, migration rollback, backup/restore distinction.
WH-B07 offline/denied/outage handling and empty states.

### 5.2 Document-checkable checks WH-T01 onwards (against pinned sources and proposed schema now)

WH-T01 import fixture restated from pinned import tests (wh-sources, WHSignatureHelperImportTests.cs lines 1-115): (a) both signatures already present (unchanged scan) → Persisted true, FullyScannedCreatedCount 0, FullyScannedChangedCount 0; (b) empty repository → Create verified called with exactly 2 signatures, FullyScannedCreatedCount 1 (only the 100% row), FullyScannedChangedCount 0; negative: partial 42.5% strength signal ("WhenGroupIsResolvedBelowFullSignal_ReportsNoChange") → group resolved but FullyScannedChangedCount 0.
WH-T02 duplicate signature name per system rejected (unique index {WHId, Name}).
WH-T03 route excludes stale link; negative: unknown-mass link is never labelled safe.
WH-T04 per-map access denial for a non-granted entity when access entries exist (WHMapAccess semantics).
WH-T05 export then re-import preserves timestamps, uncertainty and actor.
WH-T06 migration script has a paired rollback; rollback restores pre-migration schema.
WH-T07 licence header present on files deriving from Pathfinder/EVE-WHMapper structure; dependency/asset/game-data licence review is listed open, not passed.

### 5.3 Runtime-only checks (require the future app; not executed here)

WH-T08 import/export roundtrip through the running app with byte-level comparison after re-import.
WH-T09 backup creation verified by file existence and checksum; restore verified by test restore into an empty database with row-count match — backup and restore are distinct and never conflated.
WH-T10 service outage: reads served from cache, writes rejected with message, no silent data loss; recovery resumes queued edits on reconnect.
WH-T11 concurrent edit conflict surfaces both versions and invalidates stale cache on write.

### 5.4 Backup versus tested restore and service recovery

Backup creation is evidenced by artefact existence/checksum. Tested restore is evidenced by a restore run against an empty database and a row-count/content match. A backup artefact without a restore test is not recovery evidence. Service outage and recovery are tested separately: read-only cached view during outage, write rejection, queue drain on recovery.

## 6. Unresolved decisions and residual blockers

- Staleness window numeric value [T_stale] — owner decision; no game constant assumed anywhere in examples.
- Exact route-ranking weights — proposed only.
- Stack choice: maintained Pathfinder fork (PHP), maintained EVE-WHMapper fork (C#), or new implementation — evidence-linked tradeoff required; no selection claimed (brief).
- ESI scopes, token storage and encryption at rest (Pathfinder example: libsodium crypto_secretbox with 32-byte hex key, fails closed if blank — pf-sources README security hardening) — upstream identity/version verification pending.
- Dependency, asset and game-data licence checks — not performed; MIT root licence covers inspected roots only.
- No live EVE API validation, integration test or security certification has been performed (brief).

## 7. Acceptance criteria mapping

Stable identifiers WH-B01..WH-B07 and WH-T01..WH-T11; source-linked decisions throughout; WH-first scope preserved with optional cloud; exact residual blockers listed; no invented tests or approvals. This is a candidate design for review, not accepted, merged or build-ready.
