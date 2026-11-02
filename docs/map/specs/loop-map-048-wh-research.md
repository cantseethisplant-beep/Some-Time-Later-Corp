# WH RESEARCH REPORT — MAP-048: Fork versus new-code and database options

**Status:** Draft research report — not accepted, not merged, not build-ready, no implementation claimed  
**Task:** MAP-048 — Research fork versus new-code and database options  
**Claim commit:** c939860ec0a673a7175a0286b3721644e16e963b  
**Worker:** hermes-laptop-map-048-auto-20261030  
**Output path:** docs/map/specs/loop-map-048-wh-research.md  
**Input revisions:** baseline 6e023274d7cb692f36b132d980d5a335d4387897 (docs/map/specs/loop-map-042-wh-design.md); inventory 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (docs/map/research/LOCAL-RESEARCH.md, docs/map/research/NEXT-SOURCE-SNAPSHOT.json); options 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (docs/map/research/next-options-sources.md)  
**Evidence type:** Pinned primary-source text and public metadata; documented or inspected claims — not runtime verification, not accepted facts  
**Owner decisions addressed:** OD-02 (target language/runtime/stack), OD-12 (database engine)

## 1. Purpose and evidence limits

This report compares three options for the WH-first mapping/intel app using only the pinned source packets: (A) fork goryn-clade/pathfinder (PHP), (B) fork pfh59/eve-whmapper (C#/.NET), (C) new implementation informed by both, copying no substantial source. It also examines database assumptions, migration/backup boundary, dependency evidence gaps, and maintenance/porting effort.

Each finding identifies its source, the exact claim supported, status (documented/inspected/proposed/unresolved), version/validity, and what invalidates it. README feature lists are upstream-claimed shipped features, not verified behavior. No stack is selected, no savings are promised, no licence compliance is determined, and no performance or compatibility test is claimed. Root MIT notices are preserved where licence text is quoted; short quotations are used for other material.

## 2. Source inventory and pins

| Source repository | Commit | File | Pinned facts observed | Receipt SHA256 | Evidence status |
|---|---|---|---|---|---|
| goryn-clade/pathfinder | 06af7d86fe6456947fb960220c54d02a8623c0ff | LICENSE | MIT; Copyright (c) 2017 Mark Friedrich; notice must be included in all copies or substantial portions | n/a (in packet) | Inspected primary text |
| goryn-clade/pathfinder | same | README.md | Community-maintained fork of Exodus4d Pathfinder; PHP 8.5 badge; v3.0 breaking changes (PHP 7.2→8.5; DB schema v2 adds columns to system/connection/map/character; new map_group table; ESI tokens plaintext→encrypted libsodium crypto_secretbox; SMTP removed; ini→env config; WHITELIST→ALLOWLIST); security hardening (fails-closed token key, HMAC WebSocket tokens, origin checks, PKCE default, gated /setup, production guards); installation defers to pathfinder-containers | 1d7c461a1e06cb0425312d1380a34ff994632986f00728130e19c9196f9a1bd1 | Inspected public metadata (claims not verified) |
| goryn-clade/pathfinder | same | composer.json | php-64bit >=8.2; ext-pdo/openssl/curl/json/mbstring/ctype/gd/sodium (*); bcosca/fatfree-core 3.9.*; ikkez/f3-cortex dev-master#47d2596914776877ef4d87706d1faa812d1398f2; monolog ^3; firebase/php-jwt ^7; cache/redis-adapter ^1.2; react/socket ^1.16; goryn-clade/pathfinder_esi 3.0.2-beta.2 from separate VCS repo; config.audit ignores PKSA-y2cr-5h3j-g3ys; suggest ext-redis | b2bfb8f3fea25de8b6723c52fc537c5666c6974dc442e8f3b44b2b6a97d01149 | Inspected public metadata |
| pfh59/eve-whmapper | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | LICENSE | MIT; Copyright (c) 2023 pfh59 | n/a (in packet) | Inspected primary text |
| pfh59/eve-whmapper | same | README.md | Lightweight wormhole mapping/planning tool; CCP SSO, ESI API integration, multi-account; admin lists per character/alliance/corporation; per-map access lists; pilot location tracking incl. automatic via ESI; route planner over stargates and mapped wormholes; jump module with hole size/status and pilot/ship log; Docker/Kubernetes hosting; public instance whmapper.ovh; "redesigned to be easier to deploy, maintain, and use" | 0bc8d9dbb8061fa048370228c708508f472c21ab2acb2356ec6f9d99be110a81 | Inspected public metadata (claims not verified) |
| pfh59/eve-whmapper | same | src/WHMapper/WHMapper.csproj | net10.0; Microsoft.EntityFrameworkCore 10.*; Npgsql 10.*; Npgsql.EntityFrameworkCore.PostgreSQL 10.*; MudBlazor 9.9.0; Serilog; SignalR.Client 10.*; Microsoft.Extensions.Caching.StackExchangeRedis 10.*; DataProtection.StackExchangeRedis 10.*; JWT/OpenID packages 8.22.0/10.*; wh-effects.json EmbeddedResource; UserSecretsId | c6980392aa7d3e53d218067640cdebfc26ea2c8f5808b4faad524a74b24177c3 | Inspected public metadata |
| pfh59/eve-whmapper | same | deploy/docker/eve-whmapper/docker-compose.yml | postgres:17-alpine with named volume postgres:/data/postgres; redis:8-alpine, network only, no data volume evidenced; ghcr.io/pfh59/eve-whmapper:latest; placeholder EveSSO__ClientId/Secret; Logs volume | 9d3a676fcd80bde5421ebbe1abd49075443da9eb18736dce487a48dc51417187 | Inspected public metadata |
| MAP-042 baseline | 6e023274d7cb692f36b132d980d5a335d4387897 | docs/map/specs/loop-map-042-wh-design.md | Fork options A/B/C; OD-02 stack decision open; OD-12 DB engine undecided; backup creation ≠ restore verification; no restore-test evidence | — | Completed unaccepted blueprint context |
| Research inventory | 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec | LOCAL-RESEARCH.md, NEXT-SOURCE-SNAPSHOT.json | Local research policy; snapshot registry pins esi/esi-docs, pathfinder, eve-whmapper commits; six document hashes | — | Owner policy/inventory |

Validity: all upstream observations hold only at the pinned commits and file versions above. Dependency ranges (10.*, ^3, ^7) are ranges, not locks. Invalidated by newer upstream commits, supplied lockfiles, different dependency resolution, or a different stack/database choice. Note: esi/esi-docs commit 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d is pinned in the registry, but no esi-docs document was supplied to this task.

## 3. Option A — Pathfinder fork (PHP)

Runtime/stack facts (inspected):
- PHP 8.5 per README badge; composer requires php-64bit >=8.2 and ext-pdo (no driver named), ext-openssl, ext-curl, ext-json, ext-mbstring, ext-ctype, ext-gd, ext-sodium; bcosca/fatfree-core 3.9.*; firebase/php-jwt ^7.
- v3.0 breaking changes: DB schema v2 adds columns to system/connection/map/character and adds map_group table; ESI tokens at rest move from plaintext to libsodium crypto_secretbox with a 32-byte hex key, failing closed if blank; SMTP removed; config moves from ini files to environment variables; login restrictions renamed WHITELIST_* → ALLOWLIST_*.
- Installation and the v3.0 upgrade guide (backups, schema migration, env rewrite, bulk ESI token encryption) live in pathfinder-containers, which is not supplied. Deployment, migration and backup evidence for Pathfinder is therefore absent from this packet.
- DB engine: unnamed in the extract; ext-pdo is driver-agnostic. Undecided (OD-12).

README-claimed features (documented, not verified): EVE mapping tool; encrypted ESI tokens at rest; PKCE on CCP SSO enabled by default (CCP_SSO_USE_PKCE=0 can disable); WebSocket tokens HMAC-bound; WebSocket origin checks; /setup gated by PF_SETUP_ENABLED; production startup guards under APP_ENV=production.

Dependency evidence gaps: composer.lock not supplied (config.lock: true is a setting only); config.audit ignores PKSA-y2cr-5h3j-g3ys without explanation in the extract; pathfinder_esi is fetched from a separate VCS repository; assets (favicon/logo) licence unverified.

## 4. Option B — EVE-WHMapper fork (C#/.NET)

Manifest/deploy facts (inspected):
- WHMapper.csproj targets net10.0; references Microsoft.EntityFrameworkCore 10.*, Npgsql 10.*, and Npgsql.EntityFrameworkCore.PostgreSQL 10.* → PostgreSQL is the evidenced database assumption; MudBlazor 9.9.0 UI; Serilog logging; SignalR.Client 10.*; OpenTelemetry 1.18.0 family; Microsoft.Extensions.Caching.StackExchangeRedis 10.* and DataProtection.StackExchangeRedis 10.* → Redis is the evidenced cache/data-protection target; wh-effects.json is an embedded resource; UserSecretsId present (development secret store).
- docker-compose: db service postgres:17-alpine with named data volume postgres:/data/postgres; redis:8-alpine attached to the network with no data volume evidenced; whmapper image ghcr.io/pfh59/eve-whmapper:latest with placeholder EveSSO__ClientId/EveSSO__Secret and connection strings for db and redis; ./Logs volume. Compose is a deployment example, not adopted policy (MAP-042 WH-F16).

README-claimed features (documented, not verified): lightweight mapping/planning tool inspired by Pathfinder and "redesigned to be easier to deploy, maintain, and use"; CCP SSO login, ESI API integration, multi-account; administration lists per character and per alliance/corporation/character; per-map access lists; shared maps; pilot location tracking including automatic tracking via ESI; route planner over stargates and mapped wormholes; jump module with hole size/current status and per-pilot per-ship jump log; Docker/Kubernetes/other hosting; public instance at whmapper.ovh. CI/CD and SonarCloud quality-gate badges are repository metadata claims, not verified quality evidence.

Dependency evidence gaps: many package references use 10.* ranges (not pins); transitive NuGet licences unverified; wh-effects.json asset licence unverified; Docker image provenance and runtime behavior unverified.

## 5. Option C — New implementation informed by both

Per MAP-042 sections 3 and 11 (proposed, not selected): borrow structural patterns only — signature dedupe/probe-complete behavior, per-map access entries, ESI SSO/PKCE with encrypted-token-at-rest pattern, map isolation — copying no substantial source. MIT notices must be recorded and preserved for any later copying of software or substantial portions.

Preconditions: OD-02 stack decision and OD-12 DB engine decision must exist before any code fact can be claimed. This packet contains zero code or runtime evidence for a new build; "new implementation" is an unevidenced option, not a demonstrated shortcut. Porting effort is nil (nothing exists to port) but build effort is total.

## 6. Comparison (facts only)

| Dimension | Pathfinder fork | WHMapper fork | New implementation |
|---|---|---|---|
| Language/runtime | PHP 8.x + Fat Free Framework 3.9.* | .NET 10 + EF Core 10.* | Undecided (OD-02) |
| Database from pinned source | Unnamed; ext-pdo generic; schema v2/v3 + map_group | PostgreSQL via Npgsql/EF Core 10.*; compose postgres:17 + redis:8 | Undecided (OD-12) |
| Deployment evidence | External pathfinder-containers (not supplied) | Supplied docker-compose; image latest; placeholder secrets | None |
| Dependency evidence | composer.lock absent; audit-ignore entry unexplained | 10.* ranges, not pins; transitive NuGet unverified | None to audit |
| Backup/restore evidence | Upgrade guide mentions backups/migration externally | Named Postgres volume only; no restore test | None |
| README-claimed WH scope | Mapping tool; encrypted SSO tokens; PKCE | Mapping/planning; per-map access; route/jump modules | Patterns only |
| Root licence | MIT, 2017 Mark Friedrich | MIT, 2023 pfh59 | MIT notices for later copies |
| Porting effort | Whole PHP stack imported on fork | Whole .NET stack imported on fork | Nothing to port; everything to build |

## 7. Database assumptions and migration/backup boundary

Pathfinder: the engine is not named anywhere in the extract; ext-pdo names no driver, so no PostgreSQL/MySQL/SQLite assumption can be made from this packet. Schema facts are limited to v3.0 column additions on system/connection/map/character and a new map_group table. Migration and backup guidance lives in the external pathfinder-containers repository and is not supplied, so no migration step, backup schedule, or restore procedure can be cited here.

WHMapper: PostgreSQL is assumed from Npgsql + Npgsql.EntityFrameworkCore.PostgreSQL 10.*. The compose file supplies postgres:17-alpine with a named data volume and redis:8-alpine (cache/data-protection target) with no redis data volume evidenced.

Boundary: backup creation and restore verification are distinct (MAP-042 §5 R10, §9, §11). Neither packet contains restore-test evidence, row-count comparison, import into an empty database, or credentials/grant non-leakage validation. Any backup/restore claim for either fork would be new evidence, not sourced here.

## 8. Dependency, asset and legal evidence gaps

1. Pathfinder: composer.lock is not supplied, so the exact transitive dependency set is unknown despite config.lock: true. config.audit ignores PKSA-y2cr-5h3j-g3ys with no explanation in the extract. pathfinder_esi comes from a separate VCS repository.
2. WHMapper: 10.* range references resolve at build time, so the dependency surface is not pinned by csproj alone; transitive NuGet licences are unverified; wh-effects.json asset licence is unverified.
3. Both: root MIT notices do not settle transitive licences, assets (Pathfinder favicon/logo; WHMapper wh-effects.json), EVE game data, ESI terms, or the separate CCP developer agreement at https://developers.eveonline.com/license-agreement, which requires owner review; no agreement is accepted and no commercial/ISK model is approved by this packet.
4. Invalidated by: supplied lockfiles, upstream licence changes, asset-licence review, or CCP agreement review.

## 9. Maintenance, reuse and porting effort

- PHP and C# internals are incompatible; MAP-042 states they cannot be merged by assertion, and forking either imports a whole unselected stack. OD-02 must be resolved before either fork can be evaluated as a real option.
- Pathfinder is a community-maintained fork; its v3.0 introduced breaking changes across runtime, database schema, token storage (plaintext → encrypted), configuration (ini → environment), and access-list naming (WHITELIST → ALLOWLIST), plus SMTP removal. A fork inherits this migration surface.
- WHMapper's "easier to deploy, maintain, and use" description is a README claim, not evidence; CI/CD and SonarCloud badges are metadata claims, not verified quality.
- A new implementation has no code to port but also no code facts; every component would be authored against the still-undecided stack and database.

## 10. Reasoned recommendation and alternatives

This report selects no stack, promises no savings, determines no licence compliance, and claims no performance or compatibility results.

Finding: none of the three options is evidenced as build-ready from this packet. Option A lacks deployment/migration/backup evidence and a database engine. Option B has PostgreSQL and compose evidence but unverified runtime features and unverified dependency/asset licences. Option C has zero code evidence and depends on OD-02/OD-12.

Decision criteria for the owner (explicit criteria, not a selection):
1. Stack commitment exists (PHP vs .NET vs new) — gates OD-02 and every build milestone.
2. Database engine decided — gates OD-12.
3. Dependency licence audit completed for the chosen manifest (composer.lock or transitive NuGet set) — gates any copying decision.
4. Asset and EVE/ESI legal review (favicon/logo or wh-effects.json; game data; CCP agreement).
5. Restore-test evidence (backup creation is distinct from restore verification) — gates release recovery.
6. Feature coverage against the WH-first MVP, weighing README-claimed features against verified behavior.

Conditional alternatives: if PHP is selected, evaluate the Pathfinder fork only after obtaining pathfinder-containers evidence; if .NET/PostgreSQL is selected, evaluate the WHMapper fork only after dependency and asset checks; a new implementation may be considered only after OD-02/OD-12, with the §5 pattern borrowings treated as suggestions, not evidence.

## 11. Validity and invalidation

All findings are valid only at the pinned commits and file versions in section 2 and only for the inspected files. They are invalidated by any newer upstream commit; by a supplied composer.lock changing the Pathfinder dependency set; by dependency-range resolution differing from the ranges shown (10.*, ^3, ^7); by a database engine choice other than the assumptions above; by executed restore tests; by OD-02/OD-12 owner decisions; or by CCP agreement review outcomes.

## 12. Missing evidence register

1. Pathfinder deployment, migration and backup procedures (pathfinder-containers, not supplied).
2. Pathfinder database engine and driver (ext-pdo names none).
3. Pathfinder composer.lock/exact transitive dependencies and licences; meaning of audit ignore PKSA-y2cr-5h3j-g3ys.
4. Pathfinder assets (favicon/logo) licence.
5. WHMapper transitive NuGet dependency licences.
6. wh-effects.json asset licence.
7. Restore-test evidence for either database (backup creation ≠ restore verification).
8. CCP developer agreement review — owner decision, not accepted here.
9. README-claimed runtime behavior for both projects (ESI scopes/rate limits, automatic location tracking, route planner results) — unverified.
10. OD-02 stack decision and OD-12 DB engine decision — owner decisions, unresolved.

End of report. This document is research material for coordinator review; it is not accepted, merged, deployed, or certified build-ready.
