# ESI location, ship, polling and rate-limit research (MAP-044)

**Task:** MAP-044 — Research ESI location, ship, polling and rate-limit contracts  
**Claim worker:** hermes-laptop-map-044-auto-20261030  
**Claim commit:** 3904087aa16c2a43b51e065ef87a53044f7e23bf  
**Input revisions:** baseline 6e023274d7cb692f36b132d980d5a335d4387897; inventory/esi 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec  
**Output path:** docs/map/specs/loop-map-044-wh-research.md  
**Status:** research report — documented and inspected findings only; not accepted, not build-ready, no implementation claimed.

## Evidence status key

- documented-primary: quoted from pinned primary source text
- inspected: metadata/hash/structural check performed on the supplied snapshot
- proposed: this report's recommendation; not an owner decision or upstream fact
- unresolved: open owner decision or missing evidence

## 1. Purpose and evidence limits

This report is the MAP-044 deliverable: a source-linked research report on ESI location, ship, polling and rate-limit contracts for the WH-first blueprint context. It is grounded exclusively in the pinned public primary sources supplied by the guarded local reader:

- docs/map/specs/loop-map-042-wh-design.md @ 6e023274d7cb692f36b132d980d5a335d4387897 — completed UNACCEPTED WH blueprint context; owner choices/evidence unresolved, not an accepted baseline.
- docs/map/research/LOCAL-RESEARCH.md @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec — owner local-only research policy.
- docs/map/research/NEXT-SOURCE-SNAPSHOT.json @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec — snapshot inventory and receipts; pins esi/esi-docs 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d, goryn-clade/pathfinder 06af7d86fe6456947fb960220c54d02a8623c0ff, pfh59/eve-whmapper 2a493fad9acec9a8e15b619f7943ae8b6e7f30da.
- docs/map/research/next-esi-sources.md @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec — ESI pack: overview.md, rate-limiting.md, best-practices.md at esi/esi-docs 98b42d5..., plus public OpenAPI/compatibility-date/OAuth-discovery metadata with three HTTP receipts (retrieved 2026-11-02T15:49:01Z).

No network, shell, account or delegation tools were used; reading the packets is the research. No authenticated or player route was called. Distinctions between documented, inspected, proposed and unresolved are preserved throughout. Root MIT licence notice is preserved below; it does not settle transitive licences, assets, game-data rights, or the separate CCP developer agreement at https://developers.eveonline.com/license-agreement, which requires owner review and was not accepted.

> Copyright © 2015 CCP hf.
>
> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## 2. ESI compatibility and versioning contract (documented-primary)

From docs/services/esi/overview.md at esi/esi-docs 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d:

- ESI is the official RESTful API for EVE third-party development. Some endpoints are public; many require authentication via SSO, and route descriptions indicate required scopes.
- Versioning: every request may include `X-Compatibility-Date` (ISO `YYYY-MM-DD`) or the `compatibility_date` query parameter. If unset, the oldest available compatibility date is used. The date cannot be in the future or below the minimum threshold ("oldest" versions available); minimum-bar raises are communicated via dev-blogs. API changes occur at 11:00 UTC, so "today" should be approximated as `now() - 11 * 60 * 60`.
- A new compatibility date is always used for: new routes; adding or changing required request parameters; changing types of request parameters/response fields/response headers; removing request parameters; removing response fields/headers/enum values.
- Existing compatibility dates cover: adding optional request parameters; adding response fields/headers/enum values.

Snapshot reality (inspected metadata):

- `compatibility_date_requested`: 2026-08-18
- Returned `spec_info.version`: 2026-08-18; title "EVE SKINR Ingenuity (ESI) - tranquility"
- Receipts: `https://esi.evetech.net/meta/compatibility-dates` (208 bytes, sha256 7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299, retrieved 2026-11-02T15:49:01.061611Z); `https://esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18` (614672 bytes, sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6, retrieved 2026-11-02T15:49:01.330345Z); `https://login.eveonline.com/.well-known/oauth-authorization-server` (813 bytes, sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572, retrieved 2026-11-02T15:49:01.485329Z).

Validity: pinned to commit and snapshot hashes; not runtime-verified. Invalidated by any new compatibility date, dev-blog-announced minimum-threshold change, or hash mismatch on re-fetch.

## 3. Selected OpenAPI operation inventory (inspected)

The snapshot's `selected_paths` block inventories four operations relevant to location/ship. Every listed operation also declares the common parameter references AcceptLanguage, IfNoneMatch, CompatibilityDate, Tenant and IfModifiedSince; the only required path parameter is `character_id` (schema CharacterID, int64, example 90000001).

| Path | OperationId | Security (required scope) | 200 response fields (required marked *) | Cache metadata | Rate-limit extension |
|---|---|---|---|---|---|
| /characters/{character_id}/corporationhistory | GetCharactersCharacterIdCorporationhistory | none | array of { corporation_id* int64, is_deleted bool, record_id* int64, start_date* date-time } | x-cache-age 86400, x-client-cache-ttl 86400, x-server-cache-mode ttl-based, x-server-cache-ttl 86400 | none documented |
| /characters/{character_id}/location | GetCharactersCharacterIdLocation | OAuth2 esi-location.read_location.v1 | { solar_system_id* SolarSystemID, station_id? StationID, structure_id? ItemID } | x-cache-age 5, x-cache-mode event-based, x-client-cache-ttl 5 | group char-location, max-tokens 1200, window 15m |
| /characters/{character_id}/online | GetCharactersCharacterIdOnline | OAuth2 esi-location.read_online.v1 | { online* bool, last_login? date-time, last_logout? date-time, logins? int64 } | x-cache-age 60, x-cache-mode event-based, x-client-cache-ttl 60 | group char-location, max-tokens 1200, window 15m |
| /characters/{character_id}/ship | GetCharactersCharacterIdShip | OAuth2 esi-location.read_ship_type.v1 | { ship_type_id* TypeID, ship_item_id* ItemID, ship_name* string } | x-cache-age 5, x-cache-mode ttl-based, x-client-cache-ttl 5, x-server-cache-ttl 5 | group char-location, max-tokens 1200, window 15m |

All four operations annotate `x-compatibility-date: 2020-01-01` in this snapshot, distinct from the requested/returned 2026-08-18 spec date; the meaning of the per-operation annotation is taken from the spec itself, not interpreted here. Error responses use schema `Error` (`error*` string, optional `details` ErrorDetail array, optional `status` int64). The OAuth2 scheme (authorizationCode) lists `esi-location.read_location.v1`, `esi-location.read_online.v1` and `esi-location.read_ship_type.v1` among its scopes; authorize endpoint https://login.eveonline.com/v2/oauth/authorize, token endpoint https://login.eveonline.com/v2/oauth/token, revocation endpoint https://login.eveonline.com/v2/oauth/revoke (from oauth_discovery).

## 4. Cache and rate-limit behavior (documented-primary)

Rate limiting (docs/services/esi/rate-limiting.md):

- Floating window per (`rate limit group`, `userID`) bucket. Authenticated routes: `<applicationID>:<characterID>` from the access token. Non-authenticated routes: `<sourceIP>`, or `<sourceIP>:<applicationID>` if an access token is supplied.
- Rate limiting is not active on all routes yet; OpenAPI specs or HTTP response headers are the authoritative per-route source.
- Token cost per response: 2XX = 2 tokens, 3XX = 1, 4XX = 5 (429 excluded), 5XX = 0.
- Headers on limited routes: `X-Ratelimit-Group`, `X-Ratelimit-Limit` (format `150/15m`), `X-Ratelimit-Remaining`, `X-Ratelimit-Used`; on 429, also `Retry-After` (seconds until enough tokens).
- OpenAPI `x-rate-limit` extension declares `group`, `window-size`, `max-tokens`; routes in one group share window-size and max-tokens.
- Some routes carry a deeper EVE server limiter that can return 429 without rate-limit headers explaining why.

Legacy error limiting coexists with the new per-route bucket system:

- Routes without the new rate limiting remain under an older "error rate limit": at most 100 non-2xx/3xx responses per minute. After that, ESI returns 420s on all ESI routes, including routes with the new rate limiting enabled.
- Headers `X-ESI-Error-Limit-Remain` and `X-ESI-Error-Limit-Reset` are mutually exclusive with the bucket-based rate-limit headers.
- The error limit uses a fixed time frame; once reached, requests are discarded until the frame ends.

Caching (docs/services/esi/best-practices.md):

- `expires` states when the ESI cache expires; do not poll before it — circumventing ESI caching can lead to a ban.
- `last-modified` and `ETag`; `If-None-Match` on a prior value yields 304 when unchanged. Paginated resources share one `last-modified` across pages. Some resources (typically POST) provide no cache headers. Static data shares caching information.

The three location-family operations sit in the documented `char-location` group (1200 max tokens per 15m window). At the documented 2-token cost per successful call this is an arithmetic ceiling of roughly 600 successful calls per window per bucket — derived arithmetic, not an upstream promise.

## 5. What an opted-in character can supply; what is unknown between polls

With a valid character access token and the matching scope:

- `esi-location.read_location.v1`: current location — `solar_system_id` (required), plus optional `station_id` (docked station) or `structure_id` (docked structure). Event-based cache, age 5s.
- `esi-location.read_online.v1`: `online` boolean (required); optional `last_login`, `last_logout`, `logins`. Event-based cache, age 60s.
- `esi-location.read_ship_type.v1`: current ship — `ship_type_id`, `ship_item_id`, `ship_name` (all required). TTL-based cache, 5s.

Unknown between polls (documented limits only):

- Event-based caches (location, online) may change at any unannounced moment between polls; no push or streaming mechanism is evidenced in this snapshot.
- A 5s TTL means ship data may be up to 5 seconds old per headers; not independently measured.
- `solar_system_id` identifies the current system; it reveals nothing about wormhole connections, mass, or life status.
- No character-scoped jump or jump-log history is in the selected inventory, so jump events (gate, cyno, wormhole) are unknown between polls from this snapshot.
- Nothing can be claimed about state changes in any inter-poll gap; `Retry-After`, `X-Ratelimit-Remaining`, `expires` and `ETag` are the only documented signals.

No universal polling interval is prescribed here; the interval is an owner decision bounded by the documented headers, cache times and error limit.

## 6. Jump-log endpoint: evidenced or not? (inspected; snapshot-limited negative claim)

The `all_path_names` inventory includes `/universe/system_jumps` and killmail routes (e.g. `/killmails/{killmail_id}/{killmail_hash}`, character/corporation killmails), but no character-scoped jump-log endpoint — no `/characters/{character_id}/jump-log` or equivalent — appears in `selected_paths` or the full path list. Finding: the supplied snapshot does not evidence a jump-log endpoint for opted-in characters.

This negative claim is limited to this snapshot: esi/esi-docs 98b42d5..., compatibility date 2026-08-18, retrieved 2026-11-02. Absence from this public path inventory is not proof of absence from all CCP services, per the snapshot's own limitations statement.

## 7. Documented APIs versus tested calls

Documented: all claims above trace to pinned source text or public metadata with receipt hashes. Tested: none. No authenticated or player route was called; no login, app registration, token exchange or revocation was performed. Receipts establish fetch integrity (sha256/byte count), not behavior. All schemas and headers must be revalidated against the selected compatibility date before any implementation calls ESI.

## 8. Proposed compatibility/expiry/invalidation checklist (proposed — not a mandate)

Each item below is proposed for owner consideration; none is adopted policy:

1. Pin the compatibility date (2026-08-18 in this snapshot); send `X-Compatibility-Date` or `compatibility_date` on every request; never send a future date.
2. Treat any new compatibility date or dev-blog-announced minimum-threshold raise as invalidation; re-pin and re-review this report.
3. Send a User-Agent identifying the app (email and app name/version strongly preferred).
4. Cache: store `ETag`/`last-modified` per request; re-poll with `If-None-Match`/`If-Modified-Since`; treat 304 as no change; respect `expires`; never poll before it.
5. Rate limit: track `X-Ratelimit-Remaining` per bucket; slow as it approaches zero; spread requests; avoid `*/5` cron; stagger after the previous job finishes; honor `Retry-After` on 429.
6. Error limit: honor `X-ESI-Error-Limit-Reset` on 420; treat 420 as an all-routes pause; do not confuse 420 with 429 headers (mutually exclusive).
7. Treat unexplained 429s without rate-limit headers as possible deep server-side limiting; back off.
8. Auth: use the documented OAuth2 endpoints; keep tokens server-side only; call the revocation endpoint on consent revocation; refresh behavior is per SSO docs and outside this packet's verified scope.
9. Map cache modes to local staleness: event-based is not instant; treat inter-poll gaps as unknown; flag data stale when `expires` passes or validation indicates change.
10. Revalidate selected operation metadata (scopes, parameters, response fields, cache headers) against the implementation's compatibility date before any code calls ESI.

## 9. Evidence status, limitations and invalidation triggers

| Finding | Source | Status | Invalidated by |
|---|---|---|---|
| Compatibility-date contract (header/query param, oldest-default, minimum bar, 11:00 UTC, new-vs-existing change rules) | overview.md @ 98b42d5 | documented-primary | new compatibility date, dev-blog minimum change, hash mismatch |
| Returned spec version 2026-08-18; receipt hashes | openapi.json + compatibility-dates + oauth discovery receipts | inspected | re-fetch hash mismatch |
| Four location/ship operations, scopes, fields, cache metadata | selected_paths @ 98b42d5 | inspected | spec change under a new date |
| Floating-window buckets, token costs, headers, Retry-After | rate-limiting.md @ 98b42d5 | documented-primary | header/extension changes |
| Legacy 100 errors/minute → 420 on all routes; mutually exclusive headers | rate-limiting.md @ 98b42d5 | documented-primary | header/extension changes |
| Expires/last-modified/ETag/304 caching rules | best-practices.md @ 98b42d5 | documented-primary | header changes |
| Opt-in character supplies location/online/ship only; jump-log not evidenced | selected_paths + all_path_names @ 98b42d5 | inspected + snapshot-limited negative | new paths added under a new date |
| Root MIT notice (CCP hf, 2015) | LICENSE @ 98b42d5 | documented-primary | licence change |
| CCP developer agreement not reviewed/accepted | separate, not in packet | unresolved | owner review |

No claim of verified security, compatibility, test success, accepted licence/terms, or blueprint acceptance is made. MAP-042 remains UNACCEPTED context.

## 10. Open decisions carried forward (unresolved)

- OD-03 — ESI scopes, rate limits, issuer runtime contract: missing runtime evidence; blocks opt-in tracking design.
- OD-06 — numeric stale thresholds: owner placeholders.
- OD-07 — auth/token storage and revocation effectiveness: unverified.
- Polling interval: owner decision; not prescribed in this report.
- Jump-log requirement: unsupported by this snapshot; requires owner decision or additional upstream evidence.

These remain precise prerequisites; none is repaired by invention.

