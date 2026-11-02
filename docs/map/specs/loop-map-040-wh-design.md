# WH BLUEPRINT CANDIDATE — NOT ACCEPTED

**Task:** MAP-040 — Assemble WH blueprint candidate from completed parts
**Claim worker:** hermes-laptop-map-040-auto-20261030
**Claim commit:** e576ac8c2eda82d594cf3b4a6d6f36b4339daaa4
**Input revision:** 849978908daabe3d2a45f0e758625eedc4bdde30
**Output path:** docs/map/specs/loop-map-040-wh-design.md
**Status:** draft candidate for review — not accepted, not merged, not build-ready, no implementation claimed

## 1. Purpose and evidence limits

This document is the MAP-040 deliverable: a single navigable WH-first blueprint candidate assembled from the four completed, unaccepted design parts MAP-036 through MAP-039, reconciled through an explicit crosswalk, plus the pinned owner brief and inspected upstream extracts. It is a planning record only. No requirement is accepted, no stack is selected, no code is implemented, no test is executed, and nothing is deployed.

Evidence is limited to the pinned immutable inputs. Source facts cite repository commit/path/line ranges; anything uncited is proposed design. This is not runtime verification, not a licence/dependency/security audit, and not ESI validation. Cloud hosting remains an optional module behind a clean boundary and is not a mapper MVP prerequisite.

## 2. Source inventory and ID crosswalk

The four source drafts use independent local IDs and do not share identifiers. This crosswalk is the reconciliation authority; it does not claim the drafts already agree.

| Source task | Revision | Local ID scheme | Canonical MAP-040 IDs |
|---|---|---|---|
| MAP-036 | abedc17b... | WH-R01..WH-R10 requirements | WH-040-R01..WH-040-R10 |
| MAP-037 | fb2bb57a... | WH-D / WH-API domains; WH-API-01..WH-API-16 operations | WH-040-D / WH-040-API domains; WH-040-API-01..WH-040-API-16 operations |
| MAP-038 | d68d560c... | WH-SEC01..WH-SEC08 misuse cases | WH-040-SEC01..WH-040-SEC08 |
| MAP-039 | 556f3f98... | WH-B01..WH-B07 build steps; WH-T01..WH-T11 checks | WH-040-B01..WH-040-B07; WH-040-T01..WH-040-T11 |

All body references below use the canonical MAP-040 scheme.

Pinned inputs at revision 84997890...:
- docs/map/WH-FIRST-BRIEF.md — complete file; owner WH-first direction. No line-level citation claimed from this extract.
- docs/map/research/pf-sources.md — Pathfinder commit 06af7d86fe6456947fb960220c54d02a8623c0ff: LICENSE lines 1-22; README.md lines 1-61; composer.json lines 1-81; app/Model/Pathfinder/ConnectionModel.php lines 1-160 of 647; app/Model/Pathfinder/SystemSignatureModel.php lines 1-160 of 364; app/Model/Pathfinder/MapModel.php lines 1-160 of 1579.
- docs/map/research/wh-sources.md — EVE-WHMapper commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: LICENSE lines 1-22; README.md lines 1-60; src/WHMapper/WHMapper.csproj lines 1-52; src/WHMapper/Models/Db/WHSignature.cs lines 1-113 of 113; src/WHMapper/Models/Db/WHMapAccess.cs lines 1-48 of 48; src/WHMapper/Data/WHMapperContext.cs lines 1-104 of 104; deploy/docker/eve-whmapper/docker-compose.yml lines 1-46; src/WHMapper/Models/Db/WHSystemLink.cs lines 1-49 of 49; src/WHMapper/Models/Db/WHJumpLog.cs lines 1-47 of 47; src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1-43 of 43; src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115 of 115.

## 3. Reuse decision and alternatives (proposed)

MAP-036 compared Pathfinder (PHP 8.5 per README badge; composer.json requires php-64bit >=8.2, Fat Free Framework 3.9.*) with EVE-WHMapper (C# net10.0, EF Core 10.*, PostgreSQL, MudBlazor). Runtimes and dependency graphs are incompatible; PHP and C# internals must not be combined by assertion, and forking either imports a whole unselected stack.

**Proposed decision, not owner-selected:** new implementation informed by both, copying no substantial source. Borrow structural patterns only: link plus jump-log evidence (EVE-WHMapper WHSystemLink/WHJumpLog), signature dedupe/probe-complete (WHSignature HasSameContent/IsIdentified and import tests), per-map access entries (WHMapAccess), ESI SSO/PKCE and encrypted-token-at-rest pattern (Pathfinder README), map isolation (both). MIT notices are retained only if any substantial upstream block is actually copied; none is copied here.

**Alternatives:** (a) fork Pathfinder if owner selects PHP; (b) fork EVE-WHMapper if owner selects .NET. Both require separate dependency, asset and game-data licence checks plus a stack commitment that does not exist. Licence inventory status: both root licences MIT (Pathfinder 2017 Mark Friedrich; EVE-WHMapper 2023 pfh59). Transitive dependencies, assets (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json) and EVE game data/ESI terms are unverified and out of scope.

## 4. Licensing/provenance register

| Source | Commit | Extracted files (pinned paths) | Copyright holder | Licence | Notice obligation | Substantial copy in this design? | Unverified items |
|---|---|---|---|---|---|---|---|
| Pathfinder | 06af7d86fe6456947fb960220c54d02a8623c0ff | docs/map/research/pf-sources.md: LICENSE lines 1-22; README.md lines 1-61; composer.json lines 1-81; app/Model/Pathfinder/ConnectionModel.php lines 1-160 of 647; app/Model/Pathfinder/SystemSignatureModel.php lines 1-160 of 364; app/Model/Pathfinder/MapModel.php lines 1-160 of 1579 | Mark Friedrich (2017) | MIT | Copyright and permission notice must be included in all copies or substantial portions | None; structural/pattern reference only | Transitive composer dependencies; assets (favicon/logo); EVE game data/ESI terms; database/runtime specifics not named in extract |
| EVE-WHMapper | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | docs/map/research/wh-sources.md: LICENSE lines 1-22; README.md lines 1-60; src/WHMapper/WHMapper.csproj lines 1-52; src/WHMapper/Models/Db/WHSignature.cs lines 1-113 of 113; src/WHMapper/Models/Db/WHMapAccess.cs lines 1-48 of 48; src/WHMapper/Data/WHMapperContext.cs lines 1-104 of 104; deploy/docker/eve-whmapper/docker-compose.yml lines 1-46; src/WHMapper/Models/Db/WHSystemLink.cs lines 1-49 of 49; src/WHMapper/Models/Db/WHJumpLog.cs lines 1-47 of 47; src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1-43 of 43; src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115 of 115 | pfh59 (2023) | MIT | Copyright and permission notice must be included in all copies or substantial portions | None; substantial copy status | Transitive NuGet packages; embedded asset wh-effects.json; Docker images; EVE game data/ESI terms |

Both inspected roots are MIT; no root-licence conflict is established between them. Notice retention becomes obligatory only if substantial material is copied later. Dependencies, assets and EVE game data/ESI terms require separate checks before any copying; no dependency compatibility, vulnerability, or licence-conflict conclusion is drawn here.

## 5. Requirements (WH-first MVP, proposed)

Restated from MAP-036 WH-R01..R10 with origin/source, inputs, outputs and acceptance. All proposed; none accepted.

- **WH-040-R01 Shared chain map:** systems and directional links per map; links reference exactly two systems in one map; no cross-map leakage without an explicit grant. Source: Pathfinder MapModel/ConnectionModel; EVE-WHMapper WHMaps/WHSystems/WHSystemLinks.
- **WH-040-R02 Signature paste/import/edit/history:** raw scan text → unresolved/resolved signature with group/type, created/updated audit fields, history; unchanged import is a no-op; partial signal does not count as fully scanned. Source: EVE-WHMapper WHSignature.cs lines 1-113 and import tests lines 1-115; Pathfinder SystemSignatureModel.php lines 1-160.
- **WH-040-R03 Timestamps and stale observations:** every observation carries observed-at, source and uncertainty; stale-after policy TBD (placeholder, not a mandate).
- **WH-040-R04 Hole life/size/mass and jump evidence:** connection stores observed EOL status, size class, mass status; jump log links pilot, ship type/item, mass estimate, jump date; mass labelled estimate, never exact remaining mass. Source: Pathfinder ConnectionModel nominalLifespan/JUMP_MASS_BUCKETS (inspected examples only, not adopted policy); EVE-WHMapper WHSystemLink EndOfLifeStatus/Size/MassStatus; WHJumpLog lines 1-47.
- **WH-040-R05 Route planning:** ordered route over mapped connections plus stargate edges; a plan, not a guaranteed safe route; no hostile-detection promise.
- **WH-040-R06 Per-map permissions:** access entries control map access; empty-list behavior is an optional override; explicit-grant-only is the candidate default. Source: WHMapAccess.cs lines 1-48.
- **WH-040-R07 Opt-in pilot/location tracking:** tracking only for opted-in characters; consent revocable; no location stored without opt-in; no live ESI access claimed. Source: EVE-WHMapper README tracking claims (README claim, not verified behavior).
- **WH-040-R08 Notes and observed intel:** notes tied to map and optionally system, with author/timestamp; user intel, not verified detection. Source: EVE-WHMapper WHMapperContext WHNote index; Pathfinder description fields.
- **WH-040-R09 Corporation administration:** instance/admin model; at least one admin per instance; non-admin cannot alter another tenant's maps. Source: EVE-WHMapper WHMapperContext instance tables lines 1-104.
- **WH-040-R10 Backup/export/import and release recovery:** export produces a self-describing bundle; import validates before applying; backup creation and restore verification are distinct; no restore-test evidence exists. Source: Pathfinder README migration guidance (external containers repo, not in extract); EVE-WHMapper docker-compose Postgres data volume (no Redis volume evidenced in the extract).

## 6. Boundaries

**Component boundaries:** WH-040-D data domain (entities/invariants, MAP-037 section 3), WH-040-API logical operation surface, UI layer, optional cloud module behind a clean boundary. Tenant root is the instance; maps belong to instances; all other entities belong to one map. IDs are UUID text, never reused after deletion; tombstones remain in history.

**API summary (proposed logical operations, not routes):** WH-040-API-01 ReadMap (viewer); WH-040-API-02 CreateEntity (editor); WH-040-API-03 UpdateEntity (editor, expectedRevision, immutable systemId rebinding rejected); WH-040-API-04 DeleteEntity (editor, tombstone, referenced-entity guard); WH-040-API-05 PreviewScan (editor, no mutation, preview hash); WH-040-API-06 CommitScan (transactional duplicate/revision checks); WH-040-API-07 PullEvents (viewer, cursor); WH-040-API-08 PushMutations (editor, per-mutation atomic results); WH-040-API-09 ExportMap (mapAdmin, credentials excluded); WH-040-API-10 ValidateImport (mapAdmin); WH-040-API-11 CommitImport (all-or-nothing with identity remapping); WH-040-API-12 ManageGrant (mapAdmin, cannot revoke last admin without owner transfer); WH-040-API-13..16 instance/bootstrap operations, out of core MVP boundary; bootstrap actor is an owner decision. Error codes: E_FORBIDDEN, E_NOT_FOUND, E_INVALID_PAYLOAD, E_CROSS_MAP, E_CONCURRENT_REVISION, E_DUPLICATE, E_DUPLICATE_SIGNATURE, E_REFERENCED_ENTITY, E_IDEMPOTENCY_CONFLICT, E_INVALID_CURSOR, E_CURSOR_EXPIRED, E_UNSUPPORTED_VERSION, E_IMPORT_CONFLICT, E_CONFLICTING_SCAN. Authorization is checked before revealing content, before idempotency lookup, and transactionally before applying writes; E_FORBIDDEN never reveals entity existence. Concrete request/response examples (valid Signature update, E_CONCURRENT_REVISION with current entity, E_CROSS_MAP, negative shipMass rejection) are inherited unexecuted from MAP-037 section 7.

**Security boundaries (proposed):** server-side authorization for every read/write/event; clients never trusted; opt-in location/jump sharing with revocable consent; tokens server-side only, encrypted-at-rest pattern with fail-closed if key missing (Pathfinder pattern, not an adopted implementation); revocation via ESI revoke endpoint plus server-side invalidation, runtime-unverified; activity log append-only, not cascade-deleted with maps; cache keys namespaced by instance/map, invalidated on unlink/revocation/membership change; stale membership revalidation at login and periodically (interval unresolved). Misuse cases WH-040-SEC01..WH-040-SEC08 (unauthenticated read, deny-by-default, revoked token, socket replay, malicious import, cache leakage, stale membership, admin export bypass) are proposed future tests with setup/input/expected denial in MAP-038 section 17.

## 7. UI flows (proposed)

1. **Scanner paste/preview/diff/save:** paste tab-separated scan rows; preview resolves each row against existing signatures (unchanged/new/changed/below-full-strength observed-not-created); diff shows Created/Updated/CreatedBy/UpdatedBy; save persists actor, time, source-text hash and signal-strength note; unresolved rows stay "Unknow" until probed. Mirrors import-test fixtures (100% vs 42.5% signal, decimal separators).
2. **Manual chain editing:** add systems, link two selected systems, edit links, lock systems against accidental moves; every edit writes an activity-log entry; duplicate system names per map rejected.
3. **Stale signatures:** hidden from route planning unless the user explicitly accepts stale data; never supports a safety claim; stale flags are observations, not removals.
4. **Route selection:** filter excludes stale/unknown-mass/denied-access links; ranks fewest hops then fewest wormholes; displays per-leg uncertainty; explicit acceptance before sharing.
5. **Notes/intel:** attach to map plus optional system; source/time/uncertainty retained; observed events only.
6. **Offline/denied/empty:** edits queue locally and sync on reconnect; write failures fail fast with a user-visible message; denial returns a reason; empty map shows first-system prompts, no exception; no credentials or raw debug logs persisted or displayed.

## 8. Dependency-ordered build milestones (proposed)

| Milestone | Inputs | Outputs | Observable checks |
|---|---|---|---|
| WH-040-B01 Schema stubs | brief scope, pinned models | map/system/link/signature/jump-log/note/route/access stubs; MIT headers where structure reused | stubs satisfy proposed invariants; unique/cascade rules declared |
| WH-040-B02 Scanner paste/preview/diff/save | pinned import fixtures | import UI, preview hash, diff | WH-040-T01 fixture outcomes reproduced statically |
| WH-040-B03 Manual chain editing | B01 | add/link/edit/lock flows; activity log | duplicate name rejected; lock blocks deletion; log entry per edit |
| WH-040-B04 Route planner | B01, staleness policy TBD | routes over stargate plus mapped links; uncertainty display | stale/unknown-mass links excluded unless acknowledged; never "safe" |
| WH-040-B05 Access, opt-in, notes | B01 | per-map grants; opt-in consent; notes | non-granted entity denied when entries exist; no data without opt-in |
| WH-040-B06 Import/export/migration | B01-B05 | versioned export envelope v1; import validation; rollback script | export/re-import preserves timestamps, uncertainty, actor; rollback restores pre-migration schema |
| WH-040-B07 Offline/denied/outage | all prior | local queue; denial messages; cached reads | writes rejected offline with message; queue drains on reconnect; reads served from cache |

Backup creation and restore verification are distinct; B06 covers scripts only — no restore test has been executed.

## 9. Test/evidence matrix

| ID | Kind | What it checks | Pinned source | Status |
|---|---|---|---|---|
| WH-040-T01 | Document-checkable | import fixture: unchanged → no change; empty repo → only 100% row counts; partial 42.5% → resolved but not fully scanned | import tests lines 1-115 | Proposed static check |
| WH-040-T02 | Document-checkable | duplicate signature name per system rejected | WHMapperContext unique index {WHId, Name} | Proposed |
| WH-040-T03 | Document-checkable | route excludes stale link; unknown-mass link never "safe" | MAP-039 section 3.5 | Proposed |
| WH-040-T04 | Document-checkable | per-map access denial for non-granted entity when entries exist | WHMapAccess.cs lines 1-48 | Proposed |
| WH-040-T05 | Document-checkable | export/re-import preserves timestamps, uncertainty, actor | export envelope v1 proposal | Proposed |
| WH-040-T06 | Document-checkable | migration script has paired rollback restoring pre-migration schema | MAP-039 B06/T06 | Proposed |
| WH-040-T07 | Document-checkable | MIT header on files deriving from upstream structure | pf/wh LICENSE lines 1-22 | Proposed; dependency/asset/game-data review open |
| WH-040-T08..T11 | Runtime-only | import/export roundtrip byte-level; backup checksum vs test restore into empty DB; outage read-only/write-reject/queue drain; concurrent conflict shows both versions | Future app | Not executed; require built app |

A backup artefact with checksum is not recovery evidence; a tested restore into an empty database with row-count match is required and remains pending.

## 10. Contradictions resolved as labelled proposals

- **Empty access-list default:** EVE-WHMapper describes permissive "all instance members when no entries" behavior; MAP-038 proposes explicit-grant-only as candidate default with permissive behavior as optional owner override. **Proposal:** explicit-grant-only default; override requires owner decision. Not a mandate until decided.
- **PHP vs C# internals:** cannot be merged or forked jointly without stack selection. **Proposal:** new code, patterns only.
- **Stale threshold / mass buckets / route weights:** numeric values are placeholders; Pathfinder JUMP_MASS_BUCKETS are one implementation's inspected constants, not adopted game policy. **Proposal:** owner sets numerics before build acceptance.
- **Backup vs restore:** not conflated; restore verification is a separate, pending check.
- **Bootstrap authority:** WH-040-API-14 CreateMap precedes per-map mapAdmin grants; who bootstraps is an unresolved owner decision.

## 11. Missing evidence and residual blockers

1. No runtime verification of any upstream extract; no executed scripts or test runs.
2. No full dependency licence/security audit (Pathfinder composer.json; EVE-WHMapper csproj packages).
3. No asset licence check (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json).
4. No EVE game-data/ESI terms-of-use check; no live ESI validation; scopes, rate limits and issuer contract unknown.
5. No target language/runtime or stack decision by the owner.
6. No restore-test evidence; backup creation ≠ restore verification.
7. No numeric stale threshold, mass-bucket mapping or route-constraint values accepted.
8. No auth/token-storage implementation or consent-workflow evidence; token revocation effectiveness unverified.
9. Unseen handler implementations; authorization per handler must be implemented and tested.

These are precise prerequisites, not repaired by inventing facts. Independent acceptance, technical evidence and a frozen revision still govern the completion gate.

## 12. Acceptance criteria mapping

Task acceptance: exact scoped deliverable with stable identifiers, concrete examples/checks and source-linked decisions (sections 2, 4-11); WH-first scope preserved with optional cloud and exact residual blockers (sections 1, 5, 11); no invented tests or approvals (section 9 status column labels every check proposed or runtime-only). This is a candidate for review, not acceptance, merge, deployment or certification as build-ready.
