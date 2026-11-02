# MAP-036: Mapper Reuse Assessment and WH MVP Requirements

Task: MAP-036 — Mapper reuse assessment and WH MVP requirements
Claim worker: hermes-laptop-map-036-auto-20261030
Claim commit: 53df0ee9c03dbcbc26a760c571d827b9b1a4a8c3
Input revision: 849978908daabe3d2a45f0e758625eedc4bdde30
Output path: docs/map/specs/loop-map-036-wh-design.md
Status: draft proposal — not accepted, not build-ready; no implementation claimed

## 1. Purpose and evidence limits

This document is the MAP-036 deliverable: a reuse assessment of Pathfinder and EVE-WHMapper against the owner's WH-first brief, plus stable WH-R01+ requirements for a bounded wormhole-first MVP. It is a proposal only. No requirement is accepted, no stack is selected, and nothing is implemented, live-tested, accepted, or merged.

Evidence is limited to three pinned inputs at revision 849978908daabe3d2a45f0e758625eedc4bdde30:

- docs/map/WH-FIRST-BRIEF.md — owner WH-first direction; complete pinned file at this revision. No line-level citation is claimed from this extract.
- docs/map/research/pf-sources.md — Pathfinder commit 06af7d86fe6456947fb960220c54d02a8623c0ff: LICENSE, README, composer.json, ConnectionModel.php, SystemSignatureModel.php, MapModel.php.
- docs/map/research/wh-sources.md — EVE-WHMapper commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: LICENSE, README, WHMapper.csproj, WHSignature.cs, WHMapAccess.cs, WHMapperContext.cs, docker-compose.yml, WHSystemLink.cs, WHJumpLog.cs, EVEOnlineAuthenticationDefaults.cs, WHSignatureHelperImportTests.cs.

Excerpts are inspected source only: no runtime verification, no full licence/dependency/security audit, no executed upstream scripts. Baseline intent is the owner brief; every schema choice below is a proposal distinct from that baseline unless explicitly traced to a pinned source.

## 2. Source-linked upstream comparison matrix

| Feature area | Pathfinder (pinned source) | EVE-WHMapper (pinned source) | Relevance to WH MVP |
|---|---|---|---|
| Licence | MIT, Copyright 2017 Mark Friedrich (pf-sources.md LICENSE lines 1-22) | MIT, Copyright 2023 pfh59 (wh-sources.md LICENSE lines 1-22) | Both root licences MIT; notices must be retained if substantial material is copied. Dependencies/assets/game-data terms not audited here. |
| Language/runtime | README badge states PHP 8.5 (pf-sources.md README lines 1-61); composer.json requires php-64bit >=8.2, bcosca/fatfree-core 3.9.*, ext-pdo and other extensions (pf-sources.md composer.json lines 1-81). Specific database not named in the extract. | C# ASP.NET Core Web, net10.0, EF Core 10.*, PostgreSQL + Npgsql, MudBlazor UI, SignalR.Client (wh-sources.md WHMapper.csproj lines 1-52) | PHP vs C# runtime incompatibility: not internally reusable as source modules. Forking either means carrying its whole stack. |
| Map data model | MapModel: map table with scopeId, typeId, name, icon, deleteExpiredConnections, deleteEolConnections, persistentAliases, persistentSignatures, logActivity/logHistory, per-map notification URLs (pf-sources.md MapModel.php lines 1-160) | WHMapperContext: WHMaps DbSet; WHMap unique by Name; systems, links, signatures, notes, routes, jump logs all cascade under WHMapId; WHMapAccess table for per-map entity grants (wh-sources.md WHMapperContext.cs lines 1-104) | These map-scoped models do not by themselves prove access enforcement; only WHMapper access rows and README describe per-map grants. WH-first MVP can adopt WHMapper's instance/map-access separation or Pathfinder's map settings model; schema design is new work. |
| Connections/jump evidence | ConnectionModel: connection table, source/target system IDs, scope, JSON type/endpoint fields, eolUpdated, nominalLifespan, signatures and connectionLog as has-many (pf-sources.md ConnectionModel.php lines 1-160) | WHSystemLink: WHMapId, IdWHSystemFrom/To, EndOfLifeStatus, Size, MassStatus, JumpHistory collection (wh-sources.md WHSystemLink.cs lines 1-49); WHJumpLog: link id, character id, JumpDate, ship type/item/mass (wh-sources.md WHJumpLog.cs lines 1-47) | Both represent observed wormhole links with EOL status, size/mass, and jump/audit history. Link + jump-log pattern is reusable as a workflow concept, not as portable code. |
| Signatures | SystemSignatureModel: system_signature table, name/groupId/typeId/description, connectionId validated to same system, created/updated with character refs (pf-sources.md SystemSignatureModel.php lines 1-160) | WHSignature: WHId, Name (max 7 chars), Group enum, optional Type, Created/Updated with By fields, HasSameContent() dedupe, IsIdentified() probe-complete check (wh-sources.md WHSignature.cs lines 1-113) | Both track probe signatures per system with unresolved/resolved states and source attribution. WH-first MVP signature import/edit/history can be modeled on both; dedupe and probe-complete logic are testable acceptance patterns. |
| Map access/permissions | MapModel has activity-log fields and per-map Slack/Discord webhook settings; no per-map access-list rows shown in extract | WHMapAccess: WHMapId + EveEntityId/Name/Entity type + GrantedAt; README states per-map access lists; empty access list means all instance members can access (wh-sources.md WHMapAccess.cs lines 1-48) | Per-map permissions are a stated WH MVP requirement. EVE-WHMapper's explicit access-entry model is a closer structural match; Pathfinder's webhook/notification model is optional background only. |
| Opt-in tracking | MapModel fieldConf includes trackAbyssalJumps boolean flag (pf-sources.md MapModel.php lines 1-160); the README extract lines 1-61 does not mention it | README: track pilots/current locations, automatic location tracking via ESI; SSO auth defaults and token revocation endpoint (wh-sources.md EVEOnlineAuthenticationDefaults.cs lines 1-43) | Opt-in pilot/location tracking requires consent + ESI scope boundaries; neither extract proves a working tracking implementation. |
| Route planning | Route class referenced by ConnectionModel import; no route planner detail in extract | README: Route Planner Module calculates optimal paths over stargates and mapped wormholes; FibonacciHeap package referenced (WHMapper.csproj) | Route planning over mapped connections is in scope; algorithm/data structure choice is new work. |
| Auth/SSO | PKCE on CCP SSO enabled by default, ESI tokens encrypted at rest with libsodium, WS tokens HMAC-bound (pf-sources.md README security section) | CCP SSO login, ESI integration, multi-account; auth defaults with authorize/token/JWK/revoke endpoints (wh-sources.md EVEOnlineAuthenticationDefaults.cs lines 1-43) | Auth patterns are reference only. MVP auth design must be specified fresh; no live ESI validation performed. |
| Backup/restore | README v3.0 upgrade guide covers backups/schema migration/env rewrite in pathfinder-containers (external, not in extract) | docker-compose shows Postgres data volume on the db service (wh-sources.md docker-compose.yml lines 1-46); the redis service is declared without a mounted volume, so no redis volume is evidenced in the extract | Backup/export/import and release recovery are WH MVP requirements; no restore-test evidence exists in supplied sources. Backup creation and restore verification are distinct operations. |
| Tests | phpstan, phpcs, rector, php-compatibility (composer.json require-dev) | [Fact]/[Theory] test annotations and Moq imports in WHSignatureHelperImportTests covering scan import, dedupe, full-signal detection (wh-sources.md lines 1-115) | Test patterns are reference only; no tests are claimed as passing for the MVP. |

## 3. Reuse analysis: fork versus adapter versus new code

### Forking Pathfinder (PHP)

Reusable evidence: connection/link model, signature model, map settings, ESI SSO/PKCE pattern, encrypted token-at-rest pattern.

Blocker: entire stack is PHP 8.5 (README badge) / PHP >=8.2 (composer.json) plus Fat Free Framework. If the target implementation is not PHP, source modules cannot be carried. An adapter would require a full rewrite behind a compatibility layer, which is not justified by the extracts.

Verdict: not recommended as a fork unless the owner selects PHP; treat as pattern reference only.

### Forking EVE-WHMapper (C#)

Reusable evidence: WHMapperContext multi-tenant schema, WHSystemLink/WHJumpLog link+evidence model, WHSignature dedupe/probe-complete logic, WHMapAccess per-map grants, CCP SSO/OAuth defaults, Docker Postgres/Redis deployment shape.

Blocker: entire stack is C# net10.0 + EF Core + PostgreSQL + MudBlazor. If the target implementation is not C#, the same porting problem applies in reverse.

Verdict: not recommended as a fork unless the owner selects .NET; treat as pattern reference only.

### New code informed by both

Recommended as a proposed approach: define WH-first schema and services from the brief, borrowing structural patterns (link evidence, signature dedupe, per-map access, jump logs) without copying substantial source code. MIT notices are retained only if any substantial upstream block is actually copied; none is copied in this design.

Risk: PHP/C# internals cannot be merged by assertion. Dependency, asset, and game-data licence checks remain pending before any copy decision.

## 4. Dependency and licence inventory status (not an audit)

Confirmed root licences: Pathfinder MIT (commit 06af7d86...), EVE-WHMapper MIT (commit 2a493fad...). Both require copyright and permission notice retention on copies or substantial portions.

Unverified and explicitly out of scope for this task: all transitive dependencies (Pathfinder composer.json require/require-dev; EVE-WHMapper WHMapper.csproj PackageReference list), assets (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json embedded resource), and EVE game data / ESI terms of use. These require separate checks before implementation. No dependency compatibility, vulnerability, or licence-conflict conclusion is drawn here.

## 5. MVP scope and stable WH-first MVP requirements (WH-R01 onward)

### MVP scope statement (proposal)

The WH-first MVP covers wormhole mapping, intel and operations only. Cloud hosting, hardware offers, catalogue deployment, and a distributed cloud controller are optional supporting capabilities and are NOT prerequisites of the mapper MVP. Any cloud module must sit behind a clean boundary and is excluded from MVP acceptance. This scope statement is a proposal; owner approval remains open.

### WH-R01 — Shared system/connection chain map

- Origin: OB (proposed scope). Feature/source: Pathfinder MapModel + ConnectionModel maps/systems/connections; EVE-WHMapper WHMaps/WHSystems/WHSystemLinks schema.
- Inputs: system identity, connection endpoints, map scope.
- Outputs: persisted map with systems and directional links; per-map isolation.
- Acceptance: a map contains systems and links; links reference exactly two systems in the same map; no system or link leaks between maps without an explicit access grant.

### WH-R02 — Probe-signature paste/import/edit/history

- Origin: OB. Feature/source: EVE-WHMapper WHSignature (HasSameContent, IsIdentified, import tests); Pathfinder SystemSignatureModel (name/group/type/description/connectionId validation).
- Inputs: raw scan text, system id, observer id, timestamp, signal strength.
- Outputs: signature record with unresolved/resolved group, optional wormhole type, created/updated audit fields, change history.
- Acceptance: unchanged scan import reports no change; resolved-group change counts one fully-scanned creation/change; partial-signal resolution does not count as fully scanned; duplicate name/group/type within a system is detected.

### WH-R03 — Timestamps and stale observations

- Origin: OB (source/time/uncertainty retention). Feature/source: Pathfinder created/updated/eolUpdated; EVE-WHMapper Created/Updated/JumpDate.
- Inputs: observation event with observed-at time and source.
- Outputs: stored observation with observed-at, source id, stale-after policy, staleness flag.
- Acceptance: every observation carries observed-at time and source; observations older than the proposed stale threshold are marked stale (threshold value TBD by owner; proposed placeholder, not a mandate).

### WH-R04 — Observed hole life/size/mass and jump evidence

- Origin: OB. Feature/source: Pathfinder ConnectionModel nominalLifespan, EOL-related fields and JUMP_MASS_TYPES/JUMP_MASS_BUCKETS constants (ConnectionModel.php lines 1-160); these inspected upstream examples are not adopted game policy; EVE-WHMapper WHSystemLink EndOfLifeStatus/Size/MassStatus and WHJumpLog ship mass/character/jump date.
- Inputs: observed connection attributes, jump events with pilot/ship/mass.
- Outputs: connection record with life/size/mass status and linked jump-log entries.
- Acceptance: each connection stores observed EOL status, size class, mass status; jump log links pilot character, ship type/item, mass estimate, jump date; mass estimates are labelled estimates, not exact remaining mass.

### WH-R05 — Route planning over mapped connections

- Origin: OB. Feature/source: Pathfinder Route reference; EVE-WHMapper Route Planner Module over stargates and mapped wormholes.
- Inputs: origin system, destination system, map scope, jump-capable ship constraints (proposed).
- Outputs: ordered route with stargate and wormhole hops.
- Acceptance: route uses only mapped connections within scope plus known stargate edges; route output is a plan, not a guaranteed safe route; no hostile-detection promise.

### WH-R06 — Per-map permissions

- Origin: OB. Feature/source: EVE-WHMapper WHMapAccess (per-map entity grants, empty = all instance members); Pathfinder map settings/activity log.
- Inputs: map id, eve entity (character/corporation/alliance) id, grant action.
- Outputs: access-control decision per map.
- Acceptance: with no access entries, instance members can access; with entries, only explicitly granted entities access; no tenant leakage between maps in the same instance.

### WH-R07 — Opt-in pilot/location tracking

- Origin: OB (opt-in). Feature/source: EVE-WHMapper automatic location tracking via ESI, track pilots/current locations.
- Inputs: user opt-in consent, ESI token, character id.
- Outputs: current-location observation tied to consented character.
- Acceptance: tracking only for opted-in characters; consent revocable; no location data stored without opt-in; no live ESI access claimed here.

### WH-R08 — Basic notes and observed intel

- Origin: OB. Feature/source: EVE-WHMapper WHNote; Pathfinder map/system description fields.
- Inputs: map id, optional system id, note text, author, timestamp.
- Outputs: intel note attached to map/system.
- Acceptance: notes are tied to a map and optionally a system; author and timestamp retained; notes are user intel, not verified hostile detection.

### WH-R09 — Corporation administration

- Origin: OB. Feature/source: EVE-WHMapper instance admin/access tables; Pathfinder character/map scope model.
- Inputs: corporation/alliance identity, admin character, membership action.
- Outputs: admin and membership records; instance scoping.
- Acceptance: at least one admin per instance; admin can manage map access and members; non-admin cannot alter another tenant's maps.

### WH-R10 — Backup/export/import and release recovery

- Origin: OB. Feature/source: Pathfinder README backup/migration guidance (external containers repo, not in extract); EVE-WHMapper docker-compose Postgres data volume.
- Inputs: map/instance data export request, import file, restore request.
- Outputs: export bundle, import result, recovery point.
- Acceptance: export produces a self-describing bundle; import validates before applying; backup creation and restore verification are distinct operations — a backup is not verified until a restore test passes; no restore-test evidence exists yet.

## 6. Proposed approach (not owner-selected)

Recommended: new implementation informed by both upstream models, not a fork of either. Rationale: PHP and C# runtimes and dependency graphs are incompatible; forking either imports a whole stack the owner has not selected. Borrow structural patterns only: link evidence with jump logs (EVE-WHMapper), signature dedupe/probe-complete (EVE-WHMapper), per-map access entries (EVE-WHMapper), ESI SSO/PKCE and encrypted-token pattern (Pathfinder), map isolation (both). Alternatives: (a) fork Pathfinder if owner selects PHP; (b) fork EVE-WHMapper if owner selects .NET; both require separate dependency/asset/game-data licence checks and stack commitment. Owner approval of this recommendation remains open.

## 7. Precise missing evidence and residual blockers

1. No runtime verification of any upstream extract; no executed scripts, no test runs.
2. No full dependency licence/security audit for Pathfinder composer.json or EVE-WHMapper WHMapper.csproj packages.
3. No asset licence check (Pathfinder favicon/logo; EVE-WHMapper wh-effects.json).
4. No EVE game-data/ESI terms-of-use check; no live ESI validation.
5. No target language/runtime or stack decision by the owner.
6. No restore-test evidence; backup creation ≠ restore verification.
7. No numeric stale threshold, mass-bucket mapping, or route-constraint values accepted; all are proposed placeholders.
8. No auth/token-storage implementation or consent workflow evidence.

## 8. Checks performed

- Compared Pathfinder and EVE-WHMapper across map, connection, signature, access, auth, route, tracking, backup, and test domains using pinned commits and line ranges.
- Verified both root MIT licences are reproduced in the supplied extracts (22 lines each).
- Verified PHP vs C# incompatibility from composer.json and WHMapper.csproj manifests.
- Checked each WH-Rxx requirement against brief scope and pinned source fields.
- Distinguished backup creation from restore verification; marked both as unevenced.
- Verified docker-compose.yml extract evidences only a postgres named volume on the db service; no redis volume is mounted or evidenced.
- Removed unsupported SQLite claim for Pathfinder; specific database is not named in the extract.
- Corrected Pathfinder trackAbyssalJumps citation to MapModel.php; README extract does not mention it.
- Corrected Pathfinder PHP version citation: README badge for PHP 8.5; composer.json for php-64bit >=8.2, fatfree-core 3.9.*, ext-pdo.*
- Confirmed no implementation, test, acceptance, or deployment is claimed.

## 9. Handoff summary

This document is the complete MAP-036 output. It proposes stable requirements WH-R01..WH-R10 with origin/source/inputs/outputs/acceptance, a reuse tradeoff (fork/adapter/new code), a non-audit licence inventory, an explicit MVP scope statement excluding optional cloud, and precise residual blockers. No requirement is accepted; no stack is chosen; no code is implemented. The coordinator/owner must review and approve requirements and approach before any build stage. End of deliverable.
