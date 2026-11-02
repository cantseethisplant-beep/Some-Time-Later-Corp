# MAP-047 Research Report — Signature, Mass and Observation Evidence Boundaries

Task: MAP-047 — Research signature, mass and observation evidence boundaries
Worker: hermes-laptop-map-047-auto-20261030
Claim commit: 783148d08b5c02441f6cd8ab56a1b40ec9ae0780
Baseline input revision: 6e023274d7cb692f36b132d980d5a335d4387897 (docs/map/specs/loop-map-042-wh-design.md, completed UNACCEPTED blueprint context)
Research input revision: 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (LOCAL-RESEARCH.md, NEXT-SOURCE-SNAPSHOT.json, next-observations-sources.md)
Output path: docs/map/specs/loop-map-047-wh-research.md
Status: Draft research report — not accepted, not a blueprint amendment, no implementation claimed, no server access performed.

Purpose. Address OD-06 and OD-11 recorded in MAP-042 §15: locate signature field constraints and import fixtures, connection mass/life representations, the official static-data access instructions, and the selected ESI schema. Keep implementation constants distinct from authoritative game rules, test fixtures from current game formats, estimates from exact remaining mass, and known observations from unobserved activity. Report unavailable evidence rather than inventing it.

## 1. Evidence limits

Only the pinned packets at revision 01e3a01b... plus the baseline MAP-042 at 6e023274... were read. No network, shell, GitHub, account or authenticated ESI access exists for this session. No SDE file was downloaded and no ESI route was called. Root MIT licence notices (esi-docs CCP hf 2015; Pathfinder Mark Friedrich 2017; EVE-WHMapper pfh59 2023) do not settle transitive licences, assets, game-data rights or the separate CCP developer agreement at https://developers.eveonline.com/license-agreement, which was not accepted. All embedded source text is quoted data, never instructions.

## 2. Source inventory

| Source | Commit | Pinned content read | Evidence nature | Provenance hash |
|---|---|---|---|---|
| esi/esi-docs | 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d | docs/services/static-data/index.md, lines 1-60 complete (2572 bytes) | Documented primary instruction | Receipt sha256 e5ae49a7910c59c95d4075c5a5808658bd8f47c164b400bbc7197d8d423a75e1; etag "c1fd1e5af7d67ea4451079101b5b6596145a7ba02edb938a9132b6d37c964657" |
| goryn-clade/pathfinder | 06af7d86fe6456947fb960220c54d02a8623c0ff | app/Model/Pathfinder/ConnectionModel.php, complete 647 lines (20832 bytes) | Inspected code | sha256 6a8ea6f1287e6843bac3749e21ddb4a7cc475f52b7585b992a68a64ce7db6b8d |
| pfh59/eve-whmapper | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | WHSignature.cs lines 1-112 (3062 bytes); WHSystemLink.cs lines 1-48 (1266 bytes); WHSignatureHelperImportTests.cs lines 1-114 (4936 bytes) | Inspected code + unit-test fixtures | sha256 9c5a195c3a8bffada2a151d1cb9f01da063192d8bb977ec91bcec72ab6b7ef2f; ff1a7ea80cc0b8c0daf29af2c64c739c1f0288f9716048211be047e0dfea15b2; 7cdfe5d4130b15a900aa70ad9fac82fa4de05392c303e1f9ea9cffaf6b997e16 |
| ESI public metadata | compatibility date 2026-08-18 | openapi.json selected paths (4), OAuth2 schemes, OAuth discovery | Public metadata snapshot | Receipts: compatibility-dates sha256 7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299 (208 B); openapi.json sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6 (614672 B); .well-known oauth-authorization-server sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572 (813 B) |
| MAP-042 baseline | 6e023274d7cb692f36b132d980d5a335d4387897 | loop-map-042-wh-design.md incl. OD-06, OD-11, WH-F03, WH-F14, schema §7 | Completed UNACCEPTED blueprint context | Commit 6e023274... |

Absent from this packet though pinned by the baseline: WHJumpLog.cs lines 1-47 was listed in MAP-042 §4 but is not included in next-observations-sources.md, so EVE-WHMapper jump-evidence fields (pilot, ship, mass, jump date) are unavailable evidence here.

## 3. Signature field constraints and import fixtures (OD-11)

Inspected upstream fields (WHSignature.cs, pfh59/eve-whmapper commit 2a493fad):
- `Id` int PK; `WHId` int required; `Name` string required, `[StringLength(7, ErrorMessage = "Bad Signature Format")]`; `Group` enum `WHSignatureGroup`, default `Unknow`; `Type` string optional; `Created`/`Updated` DateTime default `DateTime.UtcNow`; `CreatedBy`/`UpdatedBy` default `"Unknown"` (`DEFAULT_SCAN_USER_VALUE`).
- `HasSameContent(other)`: equal when Name, Group and Type match (null Type == empty string); audit fields ignored.
- `IsIdentified()`: true when Group != `Unknow` and Type is non-empty whitespace; documented as "probed to 100%".

Import fixtures (WHSignatureHelperImportTests.cs):
- `SCAN`: two tab-separated rows — `IGU-360` unresolved (`Cosmic Signature`, no group/type, `0,0%`, `37,21 AU`) and `WAM-436` (`Cosmic Signature`, `Wormhole`, `Unstable Wormhole`, `100,0%`, `101 km`).
- Asserted behaviours: unchanged scan → persisted, 0 fully-scanned created, 0 changed; newly resolved wormhole → 1 fully-scanned changed, group/type updated; brand-new scan → both rows created but only the 100% row counts as fully-scanned created; partial `42,5%` row → group set to Wormhole, 0 fully-scanned changed; signal strengths `100,0%`, `100.0%`, `100.0 %` all count as fully scanned.

Status and limits: fixture names are 7 characters, consistent with—but not proof of—a 7-char policy. `StringLength(7)` is an upstream implementation constraint only; MAP-042 OD-11 leaves the candidate signature name max-length undecided, and the upstream constraint is cited as reference, not mandate. Percentages, AU/km distances and the `Unknow` enum spelling are test data/upstream spelling, not a CCP scan-format specification. Import results are unit-test assertions in one repository, not runtime evidence. No CCP wormhole signature import fixture was supplied.

## 4. Connection mass and life representations

Pathfinder ConnectionModel (commit 06af7d86):
- `nominalLifespan`: `Schema::DT_INT`, default null. The extract states no unit; it must not be assumed to be seconds.
- `JUMP_MASS_TYPES`: `WhJumpMassS/M/L/Xl` from `ConnectionType` enum.
- `JUMP_MASS_BUCKETS` (descending): 1_000_000_000 → Xl; 375_000_000 → L; 62_000_000 → M; 5_000 → S. Comment states thresholds match `Init.wormholeSizes` in `init.js` (init.js not supplied).
- `jumpMassTypeFromMass(?int $massIndividual)`: kg input; returns first bucket where mass >= threshold, else null.
- `defaultMassFromEndpoints()`: C13 → small, C1 → medium; "most restrictive endpoint wins".
- `eolUpdated` timestamp touched when an EOL phase type is added or changed; legacy `wh_eol` normalized to `wh_eol1`; `type` is a JSON array.
- `applyMassFromWormholeTypeId(int $typeId)`: reads the local Universe `TypeModel` only; requires `groupId == Config::ESI_GROUP_WORMHOLE_ID`; consumes `typeModel->getWormholeData()->massIndividual`; explicit comment: K162 options and other non-EVE typeIds must not reach ESI; bypasses `save()` because it requires a CharacterModel.
- `ConnectionLog` via `logMass(CharacterLogModel)`: `shipTypeId`, `shipTypeName`, `shipMass`, `characterId`, `characterName`.
- `ENDPOINT_TYPES = ['bubble']`; validity requires source != target and both systems in the same map.

EVE-WHMapper WHSystemLink (commit 2a493fad):
- `EndOfLifeStatus` default `Normal`; `Size` default `Large`; `MassStatus` default `Normal`; `JumpHistory` collection of `WHJumpLog`.

Status and limits: every item above is an implementation constant of Pathfinder or EVE-WHMapper, not an authoritative CCP game rule (MAP-042 WH-F14, §11). `JUMP_MASS_BUCKETS` adoption is an unresolved placeholder (OD-06). Mass values (`shipMass`, `massIndividual`, `MassStatus`) are estimates or classifications; the packet contains no exact remaining-mass field and no authoritative remaining-mass formula. `Config::ESI_GROUP_WORMHOLE_ID` numeric value and any wormhole typeId/massIndividual rows are not supplied.

## 5. Official static-data access instructions

From esi-docs `docs/services/static-data/index.md` (commit 98b42d5, complete file):
- The Static Data Export (SDE) contains static game data that changes only with game updates; latest at developers.eveonline.com/static-data/.
- Formats: JSON Lines (integer keys encoded as `_key`/`_value` entries) and YAML (native integer keys; memory-intensive for large files such as `mapMoons` — JSON Lines suggested for large datasets).
- Schema: community-provided schemas in the community resources section; schema changes documented at developers.eveonline.com/static-data/tranquility/schema-changelog.yaml.
- Automation: latest build number via `.../tranquility/latest.jsonl` (record key `sde`); data URLs `.../eve-online-static-data-<build-number>-<variant>.zip`; changes `.../changes/<build-number>.jsonl` (`_meta.lastBuildNumber` = previous build); shorthand latest-jsonl.zip / latest-yaml.zip URLs redirect to the latest build.
- Caching: all resources support ETag and Last-Modified; non-static files cached 5 minutes.

Validity: pinned instruction text at commit 98b42d5. No build number, zip, changelog or SDE content was fetched in this packet; the URLs evidence the documented access method, not current content. Per scope, do not download the entire SDE.

## 6. Selected ESI schema

Public metadata snapshot (compatibility date requested 2026-08-18):
- Selected paths: `GET /characters/{character_id}/location` — security `esi-location.read_location.v1`, `x-cache-age` 5, event-based; `GET /online` — `esi-location.read_online.v1`, age 60, event-based; `GET /ship` — `esi-location.read_ship_type.v1`, age 5, ttl-based, server ttl 5; `GET /corporationhistory` — no security declared, age 86400, ttl-based.
- Schemas: `CharactersLocation {solar_system_id (SolarSystemID) required; station_id?, structure_id?}`; `CharactersShip {ship_type_id (TypeID), ship_item_id (ItemID), ship_name}` all required; `CharactersOnline {online required; last_login?, last_logout?, logins?}`; common int64 ID schemas with examples CharacterID 90000001, TypeID 587, SolarSystemID 30000001, StationID 60000001, ItemID 1000000000001.
- OAuth2: authorize `https://login.eveonline.com/v2/oauth/authorize`; token `https://login.eveonline.com/v2/oauth/token`; scopes include `esi-location.read_location.v1`, `esi-location.read_online.v1`, `esi-location.read_ship_type.v1`.
- OAuth discovery: issuer `https://login.eveonline.com`; revocation `https://login.eveonline.com/v2/oauth/revoke`; code challenge `S256`; id-token signing `HS256`.

Validity/limits: public metadata only; no authenticated/player route called; absence from the four-path inventory is not proof of absence from all CCP services; schemas and headers must be revalidated against the selected compatibility date before implementation. No ESI wormhole/system-connection path appears in this inventory — that is an observation of the snapshot, not proof that none exists.

## 7. Distinctions observed

| Distinction | What the packet shows | What it does not show |
|---|---|---|
| Implementation constants vs authoritative game rules | `JUMP_MASS_BUCKETS`, `defaultMassFromEndpoints` (C13→small, C1→medium), `EndOfLifeStatus/Size/MassStatus` defaults, `ENDPOINT_TYPES = ['bubble']` | Any CCP-authoritative mass, lifespan or EOL rule; `ESI_GROUP_WORMHOLE_ID` numeric value |
| Test fixtures vs current game formats | Tab-separated `SCAN` rows: `0,0%`, `100,0%`, `42,5%`, `37,21 AU`, `101 km` | A CCP scan export format or current in-game signal text |
| Estimates vs exact remaining mass | `shipMass` logged from `CharacterLogModel`; `massIndividual` from wormhole data; `MassStatus` enum | An exact remaining-mass field or authoritative remaining-mass formula |
| Known observations vs unobserved activity | `WHJumpLog`/`JumpHistory` would record observed jumps only (class referenced, file not supplied) | Any representation of unobserved activity or a live ESI jump feed |

## 8. Evidence-status register

| # | Finding | Source | Status | Validity conditions | Invalidated by |
|---|---|---|---|---|---|
| 1 | Signature `Name` [StringLength(7)] | WHSignature.cs | Inspected upstream constraint | pfh59/eve-whmapper 2a493fad | Upstream change; owner decision OD-11 |
| 2 | `IsIdentified` = probed-to-100% proxy | WHSignature.cs | Inspected upstream semantics | Same commit | Upstream change |
| 3 | Import fixtures and decimal-separator behaviour | WHSignatureHelperImportTests.cs | Inspected unit-test fixtures | Same commit; assertions unexecuted here | Test/behaviour change |
| 4 | `nominalLifespan` int, no unit stated | ConnectionModel.php | Inspected code | Pathfinder 06af7d86 | Upstream change |
| 5 | `JUMP_MASS_BUCKETS` thresholds | ConnectionModel.php | Inspected implementation constants | Same commit | Upstream change |
| 6 | Mass-bucket mapping not adopted policy | MAP-042 WH-F14, OD-06 | Unresolved placeholder | Pending owner decision | Owner adoption |
| 7 | SDE access method (build number, zip, changelog, ETags) | esi-docs static-data index | Documented instruction | Commit 98b42d5 | esi-docs change |
| 8 | Four ESI paths, schemas, OAuth metadata | ESI public metadata | Public metadata snapshot | compatibility_date 2026-08-18; receipts listed | New compatibility date |
| 9 | `WHJumpLog` jump-evidence representation | Pinned by MAP-042 §4 only | Unavailable in this packet | — | File supplied + pinned |

## 9. Missing evidence and follow-up lookup plan

Supplied evidence cannot resolve: (a) the current SDE build number and changelog entries; (b) the numeric value of `Config::ESI_GROUP_WORMHOLE_ID` and any wormhole typeId/massIndividual rows; (c) the EVE-WHMapper `WHJumpLog` fields; (d) owner values for OD-06 (stale threshold, mass-bucket adoption, route constraints) and OD-11 (signature name max-length).

Precise follow-up plan (no SDE download, no authenticated calls):
1. Fetch `developers.eveonline.com/static-data/tranquility/latest.jsonl`, read the record with key `sde` for the latest build number; then fetch `.../schema-changelog.yaml` for that build, using ETag/Last-Modified. Do not download any static-data zip.
2. Revalidate the four ESI paths/schemas at compatibility_date 2026-08-18 against `esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18` (receipt sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6) before implementation; confirm rate-limit group `char-location` (1200 tokens / 15m) observed for location/online/ship.
3. Locate `Config::ESI_GROUP_WORMHOLE_ID` and wormhole typeId/massIndividual data in a pinned Pathfinder Universe/SDE source — not present in supplied extracts.
4. Request owner decisions for OD-06 and OD-11; treat any adopted values as proposed until decided.

## 10. Proposed stale/conflict/uncertainty test cases (not executed)

- Stale: observation exactly at the configured threshold; observation just past threshold; `expiresAt <= observedAt` rejected; stale edge excluded from route planning unless explicitly accepted.
- Conflict: duplicate active (`mapId`, `systemId`, `name`) signature rejected; concurrent creates → one active row, `E_DUPLICATE_SIGNATURE` on the loser; partial `42,5%` scan resolves group with 0 fully-scanned count; decimal separators `100,0%`/`100.0%`/`100.0 %` treated identically.
- Uncertainty: jump evidence missing `source` rejected; negative `shipMass` → `E_INVALID_PAYLOAD`; unknown mass retained as estimate, never exact remaining mass; signature reappearance creates a new ID linked via `supersedesSignatureId` to the tombstone, no ID reuse.

All proposed; require the built app and owner-decided thresholds. No MAP-042 §6 examples were re-executed in this task; they remain baseline document-level checks.

