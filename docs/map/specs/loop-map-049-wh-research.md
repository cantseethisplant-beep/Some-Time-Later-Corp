# MAP-049 — Research evidence register and proposed blueprint amendments

**Task:** MAP-049 — Assemble research evidence register and proposed blueprint amendments  
**Claim worker:** hermes-laptop-map-049-auto-20261030  
**Claim commit:** 485f359c495fe25f9856c2140047557e63e5d731  
**Task status:** completed draft for review — not accepted, not merged, not build-ready  
**Output path:** docs/map/specs/loop-map-049-wh-research.md  
**Loop:** WH research v1, cycle 207, research step 7

## 1. Purpose and evidence limits

This report is the MAP-049 deliverable: a consolidated evidence register and proposed-blueprint-amendment record synthesizing six completed, UNACCEPTED research reports (MAP-043 through MAP-048) against the MAP-042 WH blueprint candidate (commit 6e023274..., unaccepted context only). It is produced solely from pinned primary-source packets supplied by the local guarded reader. No network, shell, account, delegation or server tools were used; no authenticated route was called, no app registered, no terms accepted, and no runtime behavior tested. Nothing here certifies security, compatibility, licence acceptance, or build readiness. Source claims are labelled documented-primary, inspected-source, proposed, or unresolved; owner choices and runtime evidence remain distinct from researched claims. The MAP-042 blueprint is quoted context, not a mutable baseline.

## 2. Evidence status key and source inventory

Status labels: documented-primary (quoted pinned source text), inspected-source (public code/metadata read in full), proposed (this report's framing, not an owner decision), unresolved (missing evidence or open owner decision).

| # | Source | Revision | Pin / receipt | Role |
|---|---|---|---|---|
| S1 | esi/esi-docs | 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d | NEXT-SOURCE-SNAPSHOT pin; receipts in MAP-043/044/047 packets | SSO docs, ESI overview, rate-limiting, best-practices, static-data |
| S2 | goryn-clade/pathfinder | 06af7d86fe6456947fb960220c54d02a8623c0ff | NEXT-SOURCE-SNAPSHOT pin | Pathfinder composer.json, composer.lock projection, ConnectionModel |
| S3 | pfh59/eve-whmapper | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | NEXT-SOURCE-SNAPSHOT pin | EVE-WHMapper token provider, access handlers, WHMapAccess, signatures, links |
| S4 | ESI public metadata | compatibility date 2026-08-18 | compatibility-dates sha256 7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299 (208 B); openapi.json sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6 (614,672 B); oauth-authorization-server sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572 (813 B); fetched 2026-11-02T15:49:01Z | ESI compatibility date, OpenAPI paths, OAuth discovery |
| S5 | MAP-042 baseline | 6e023274d7cb692f36b132d980d5a335d4387897 | — | Unaccepted blueprint context only |

Six research reports: MAP-043 @ 5b46475c3852fc61de308a8af10426e2625dcb78; MAP-044 @ 6b5f1853fa1f65509a222d6724795dec3f3f5f6f; MAP-045 @ 7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d; MAP-046 @ d30912f7966fe966e1db29789d16452f7ec33474; MAP-047 @ d23a249231ca47e97f38889c06da78bb5a8ff599; MAP-048 @ d5299f396d5878ca6b436aa49dede05b11b4f8dd — all completed, unaccepted review material only; source claims, not independently verified facts.

## 3. Evidence register (stable IDs)

Entries below are normalized coordinator-reviewed research records, not independently accepted facts or runtime evidence. The original native register and critic findings are retained.

### E01

- **Claim:** EVE SSO is OAuth 2.0; scopes user-consented; client secret private; redirect URLs must match registration
- **Source:** S1 docs/services/sso/index.md lines 1-221 (section-level Terms citation; exact Terms line range not supplied)
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 98b42d5, retrieved 2026-11-02T15:49:02Z
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** vendor doc change
- **Affected:** OD-03, MAP-042 §11

### E02

- **Claim:** PKCE: 32-byte random verifier, base64url; challenge = SHA256(verifier) base64url no padding, method S256; no client secret; endpoints login.eveonline.com/v2/oauth/{authorize,token}
- **Source:** S1 snippets/sso/authorization-code-pkce.py lines 1-71
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 98b42d5, retrieved 2026-11-02T15:49:03Z
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** vendor doc change
- **Affected:** OD-03

### E03

- **Claim:** The supplied JWT sample selects JWKS key by kid/alg; jwt.decode verifies its issuer allowlist and EVE Online audience; the wrapper separately checks this client_id in aud. Metadata cache is 300 seconds in that sample. The sample contains a legacy-looking issuer string; discovery currently names https://login.eveonline.com. These are inspected/documented references, not a tested validator
- **Source:** S1 validate-jwt-token.py lines 1-86 + index.md
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 98b42d5; snippets retrieved 2026-11-02T15:49:03Z; index.md retrieved 2026-11-02T15:49:02Z
- **Status:** documented-primary
- **Contradictions:** Do not use OAuth discovery ID-token/client-auth HS256 fields as the access-token signing policy. Review issuer/key/algorithm policy for the actual token type; no snippet was executed
- **Invalidation:** doc/key change
- **Affected:** OD-03, OD-07

### E04

- **Claim:** Refresh token long-lived, usable until user revokes application access; access token time-limited, replaced via refresh
- **Source:** S1 index.md lines 1-221 pinned; Terms exact line range not supplied — section-level only
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 98b42d5, retrieved 2026-11-02T15:49:02Z
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** vendor policy change
- **Affected:** OD-03, OD-14

### E05

- **Claim:** OAuth discovery: revocation_endpoint https://login.eveonline.com/v2/oauth/revoke; auth methods client_secret_basic/post/jwt; code challenge S256 only; issuer https://login.eveonline.com
- **Source:** S4 oauth discovery snapshot sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572, 813 B, fetched 2026-11-02T15:49:01Z
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** Not directly observed; synthesis/gap recorded in MAP-043 at 5b46475c3852fc61de308a8af10426e2625dcb78; no runtime measurement
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** endpoint rotation
- **Affected:** OD-03, OD-07

### E06

- **Claim:** EVE-WHMapper EveOnlineTokenProvider: in-memory ConcurrentDictionary keyed by AccountId; per-account SemaphoreSlim; IsTokenExpire 5-minute skew margin; refresh via refresh_token grant with Basic auth, rotates refresh token, Expiry = now + ExpiresIn; RevokeToken POSTs token_type_hint=refresh_token, clears cache only on success; no access-token revocation path
- **Source:** S3 src/WHMapper/Services/EveOAuthProvider/Services/EVEOnlineTokenProvider.cs lines 1-162
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 2a493fad, retrieved 2026-11-02T15:49:03Z
- **Status:** inspected-source
- **Contradictions:** Upstream remote refresh-token revocation and local logout/cache invalidation are distinct; failed remote revocation does not prove local logout. See section 4 item 3
- **Invalidation:** upstream code change
- **Affected:** OD-07, MAP-042 §11

### E07

- **Claim:** Revocation failure leaves local cache intact: remote revocation ≠ guaranteed local logout; failed revocation leaves local/remote divergence
- **Source:** S3 same file, lines 1-162
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 2a493fad, retrieved 2026-11-02T15:49:03Z
- **Status:** inspected-source
- **Contradictions:** Upstream remote refresh-token revocation and local logout/cache invalidation are distinct; failed remote revocation does not prove local logout. See section 4 item 3
- **Invalidation:** upstream code change
- **Affected:** OD-07, OD-09

### E08

- **Claim:** No consent-status API evidenced; player revokes consent at SSO at any time (docs)
- **Source:** S1 index.md lines 1-221 pinned; Terms exact line range not supplied — section-level only
- **Source report:** [MAP-043](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/5b46475c3852fc61de308a8af10426e2625dcb78/docs/map/specs/loop-map-043-wh-research.md)
- **Scope:** auth/SSO tokens
- **Observed:** commit 98b42d5, retrieved 2026-11-02T15:49:02Z
- **Status:** documented-primary
- **Contradictions:** Upstream remote refresh-token revocation and local logout/cache invalidation are distinct; failed remote revocation does not prove local logout. See section 4 item 3
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-14

### E09

- **Claim:** Compatibility-date contract: X-Compatibility-Date or query param; oldest available date if unset; minimum bar via dev-blog; changes at 11:00 UTC; new date required for new/changed route params/types/removals
- **Source:** S1 docs/services/esi/overview.md
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** commit 98b42d5; no per-file receipt timestamp supplied
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** new compatibility date or minimum-threshold change
- **Affected:** OD-03

### E10

- **Claim:** Snapshot reality: spec_info.version 2026-08-18, title "EVE SKINR Ingenuity (ESI) - tranquility"; receipts compatibility-dates sha256 7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299 (208 B); openapi.json sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6 (614,672 B); oauth-authorization-server sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572 (813 B); fetched 2026-11-02T15:49:01Z
- **Source:** S4 https://esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18; SHA-256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6; discovery SHA-256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** ESI compatibility date 2026-08-18; specification reports 2026-08-18; fetched 2026-11-02T15:49:01.330345+00:00
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** re-fetch hash mismatch
- **Affected:** OD-03

### E11

- **Claim:** Three location-family operations are in the documented char-location group: /characters/{character_id}/location (esi-location.read_location.v1, solar_system_id required, station_id/structure_id optional, event-based age 5s), /characters/{character_id}/online (read_online.v1, online required, age 60s), /characters/{character_id}/ship (read_ship_type.v1, ship_type_id/ship_item_id/ship_name required, TTL-based age 5s). /characters/{character_id}/corporationhistory is unauthenticated, age 86400, with no documented rate-limit extension — not part of char-location. At the documented 2-token cost per successful call, the char-location group (1200 max tokens per 15m window) implies an arithmetic ceiling of roughly 600 successful calls per window per bucket — derived arithmetic, not an upstream promise
- **Source:** S4 https://esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18; SHA-256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6; discovery SHA-256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572; S1 rate-limiting.md at 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** ESI compatibility date 2026-08-18; specification reports 2026-08-18; fetched 2026-11-02T15:49:01.330345+00:00
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** spec change under new date
- **Affected:** OD-03, OD-06

### E12

- **Claim:** Rate limiting: floating window per (group, userID); 2XX=2 tokens, 3XX=1, 4XX=5, 5XX=0; headers X-Ratelimit-Remaining etc., Retry-After on 429
- **Source:** S1 rate-limiting.md
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** commit 98b42d5; no per-file receipt timestamp supplied
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** header/extension change
- **Affected:** OD-03, OD-06

### E13

- **Claim:** Legacy error limit: 100 non-2xx/3xx/min → 420 on all routes; headers mutually exclusive with bucket headers
- **Source:** S1 rate-limiting.md
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** commit 98b42d5; no per-file receipt timestamp supplied
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-06

### E14

- **Claim:** Caching: expires/last-modified/ETag; If-None-Match → 304; never poll before expires
- **Source:** S1 best-practices.md
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** commit 98b42d5; no per-file receipt timestamp supplied
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-06

### E15

- **Claim:** Jump-log: snapshot inventories no /characters/{character_id}/jump-log or equivalent; all_path_names includes /universe/system_jumps and killmails but no character-scoped jump-log. Negative claim limited to this snapshot; absence is not proof of absence from all CCP services
- **Source:** S4 https://esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18; SHA-256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6; discovery SHA-256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572
- **Source report:** [MAP-044](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6b5f1853fa1f65509a222d6724795dec3f3f5f6f/docs/map/specs/loop-map-044-wh-research.md)
- **Scope:** ESI location/ship polling and rate limits
- **Observed:** ESI compatibility date 2026-08-18; specification reports 2026-08-18; fetched 2026-11-02T15:49:01.330345+00:00
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** new paths under new date
- **Affected:** OD-03, jump-log requirement

### E16

- **Claim:** Pathfinder composer.json: license MIT; php-64bit >=8.2; ext-pdo/openssl/curl/json/mbstring/ctype/gd/sodium "*"; prod deps include fatfree-core 3.9.*, f3-cortex dev-master#commit, f3-sheet 0.4.*, f3-cron 1.3.*, monolog ^3, firebase/php-jwt ^7, cache adapters, react packages; config.audit.ignore ["PKSA-y2cr-5h3j-g3ys"]; config.allow-plugins dealerdirect/phpcodesniffer-composer-installer
- **Source:** S2 composer.json lines 1-80
- **Source report:** [MAP-045](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d/docs/map/specs/loop-map-045-wh-research.md)
- **Scope:** Pathfinder/EVE-WHMapper dependencies and licences
- **Observed:** commit 06af7d86, retrieved 2026-11-02T15:49:05.695523Z
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** upstream manifest change
- **Affected:** OD-04, OD-05

### E17

- **Claim:** composer.lock projection: locked exact versions incl. fatfree-core 3.9.3 (GPL-3.0), f3-cortex dev-master (GPL-3.0), f3-sheet v0.4.3 (GPL-3.0), f3-cron v1.3.0 (GPL-3.0-only), html-to-markdown 5.2.3 (MIT), monolog 3.12.1 (MIT), firebase/php-jwt v7.2.1 (BSD-3-Clause); transitive GPL/LGPL inferred. Packet labels projection "not independently verified"; declared SPDX labels not inspected licence files
- **Source:** S2 composer.lock projection lines 1-744
- **Source report:** [MAP-045](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d/docs/map/specs/loop-map-045-wh-research.md)
- **Scope:** Pathfinder/EVE-WHMapper dependencies and licences
- **Observed:** commit 06af7d86, retrieved 2026-11-02T15:49:06.142709Z
- **Status:** inspected-source
- **Contradictions:** MAP-048 says the lockfile is absent from its options packet; MAP-045 separately supplies a lock projection. Batch-wide exact package metadata is available, but individual licences and legal compatibility remain unchecked
- **Invalidation:** lock hash mismatch or supplied lockfile difference
- **Affected:** OD-04

### E18

- **Claim:** EVE-WHMapper WHMapper.csproj: net10.0; EF Core 10.*, Npgsql 10.*, Npgsql.EntityFrameworkCore.PostgreSQL 10.* → PostgreSQL evidenced; MudBlazor 9.9.0; Redis cache/dataprotection 10.*; wh-effects.json EmbeddedResource; global.json pins SDK 10.0.100. No .NET lock supplied
- **Source:** S3 WHMapper.csproj lines 1-51
- **Source report:** [MAP-045](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d/docs/map/specs/loop-map-045-wh-research.md)
- **Scope:** Pathfinder/EVE-WHMapper dependencies and licences
- **Observed:** commit 2a493fad, retrieved 2026-11-02T15:49:06.542909Z
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** upstream csproj change
- **Affected:** OD-04, OD-12

### E19

- **Claim:** Root MIT notices ×3 (esi-docs CCP hf 2015; Pathfinder Mark Friedrich 2017; WHMapper pfh59 2023): each covers its own repository only. esi-docs docs/resources/license.md: developer agreement must be signed before third-party apps; agreement https://developers.eveonline.com/license-agreement, unsigned, no commercial/ISK model approved
- **Source:** S1 license.md lines 1-3 + root LICENSE texts
- **Source report:** [MAP-045](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d/docs/map/specs/loop-map-045-wh-research.md)
- **Scope:** Pathfinder/EVE-WHMapper dependencies and licences
- **Observed:** license.md retrieved 2026-11-02T15:49:07.347027Z; root LICENSE texts quoted inline, no separate fetch receipt
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** licence change / agreement review
- **Affected:** OD-05

### E20

- **Claim:** Root MIT does not settle transitive licences, assets (favicon/logo, wh-effects.json), EVE game data, ESI terms, CCP agreement
- **Source:** MAP-045 §3.5 framing
- **Source report:** [MAP-045](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d/docs/map/specs/loop-map-045-wh-research.md)
- **Scope:** Pathfinder/EVE-WHMapper dependencies and licences
- **Observed:** Not directly observed; synthesis/gap recorded in MAP-045 at 7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d; no runtime measurement
- **Status:** proposed
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-04, OD-05

### E21

- **Claim:** EveMapperRequirementHandlerBase: NameIdentifier must parse as int; client_uid cookie client-supplied, not trusted alone; primary-account path via GetAccountsAsync/GetPrimaryAccountAsync; null-primaryAccount falls through to direct authenticated-character authorization (no return in null branch); no try/catch around IsAuthorizedAsync; helper exceptions abort request
- **Source:** S3 Services/EveMapper/AuthorizationPolicies/EveMapperRequirementHandlerBase.cs lines 1-65
- **Source report:** [MAP-046](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d30912f7966fe966e1db29789d16452f7ec33474/docs/map/specs/loop-map-046-wh-research.md)
- **Scope:** map access/bootstrap/membership
- **Observed:** commit 2a493fad, retrieved 2026-11-02 between 15:49:07 and 15:49:09 UTC
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** supplied helper implementation differing
- **Affected:** OD-09, OD-10

### E22

- **Claim:** EveMapperAccessHandler / EveMapperAdminHandler (21 lines each): thin delegates to IEveMapperAccessHelper.IsEveMapperUserAccessAuthorized / IsEveMapperAdminAccessAuthorized; helper bodies, policy registration, endpoint mapping absent
- **Source:** S3 EveMapperAccessHandler.cs lines 1-21; EveMapperAdminHandler.cs lines 1-21
- **Source report:** [MAP-046](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d30912f7966fe966e1db29789d16452f7ec33474/docs/map/specs/loop-map-046-wh-research.md)
- **Scope:** map access/bootstrap/membership
- **Observed:** commit 2a493fad, retrieved 2026-11-02 between 15:49:07 and 15:49:09 UTC
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-09

### E23

- **Claim:** WHMapAccess: grant row Id/WHMapId/EveEntityId/EveEntityName/EveEntity/GrantedAt; comment: no entries ⇒ all instance members; ≥1 entry ⇒ explicit grants only. Upstream permissive default; enforcement query/middleware not supplied
- **Source:** S3 Models/Db/WHMapAccess.cs lines 1-47
- **Source report:** [MAP-046](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d30912f7966fe966e1db29789d16452f7ec33474/docs/map/specs/loop-map-046-wh-research.md)
- **Scope:** map access/bootstrap/membership
- **Observed:** commit 2a493fad, retrieved 2026-11-02 between 15:49:07 and 15:49:09 UTC
- **Status:** inspected-source
- **Contradictions:** Upstream empty-list permissiveness differs from the blueprint proposed explicit-grant default; this is a policy choice, not evidence that enforcement has been tested
- **Invalidation:** enforcement implementation reading rows differently
- **Affected:** OD-13, MAP-042 §5 R06

### E24

- **Claim:** InstanceRegistrationHelper: requires authenticated primary account; owner character/corporation/alliance; corporation requires CorporationId>0, alliance AllianceId>0; creation lock and CanRegisterAsync (one instance per owner entity); creating character id/name recorded. Tests mock all dependencies; nothing executed
- **Source:** S3 Services/EveMapper/InstanceRegistrationHelper.cs lines 1-119
- **Source report:** [MAP-046](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d30912f7966fe966e1db29789d16452f7ec33474/docs/map/specs/loop-map-046-wh-research.md)
- **Scope:** map access/bootstrap/membership
- **Observed:** commit 2a493fad, retrieved 2026-11-02 between 15:49:07 and 15:49:09 UTC
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-10

### E25

- **Claim:** No first-owner seed or initial-admin designation visible; cache invalidation on grant revocation/membership change/logout absent from pack
- **Source:** MAP-046 §3.3/§3.6 gap
- **Source report:** [MAP-046](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d30912f7966fe966e1db29789d16452f7ec33474/docs/map/specs/loop-map-046-wh-research.md)
- **Scope:** map access/bootstrap/membership
- **Observed:** Not directly observed; synthesis/gap recorded in MAP-046 at d30912f7966fe966e1db29789d16452f7ec33474; no runtime measurement
- **Status:** unresolved
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-10, OD-07, OD-09

### E26

- **Claim:** WHSignature: Name StringLength(7) "Bad Signature Format"; Group default "Unknow"; Type optional; HasSameContent compares Name/Group/Type ignoring audit fields; IsIdentified = Group != Unknow and Type non-empty ("probed to 100%"). Upstream constraint only; MAP-042 OD-11 leaves candidate max-length undecided
- **Source:** S3 Models/Db/WHSignature.cs lines 1-112
- **Source report:** [MAP-047](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d23a249231ca47e97f38889c06da78bb5a8ff599/docs/map/specs/loop-map-047-wh-research.md)
- **Scope:** signature/mass/observation boundaries
- **Observed:** commit 2a493fad; no per-file retrieval timestamp supplied in packet
- **Status:** inspected-source
- **Contradictions:** Upstream constraints/test fixtures are not authoritative universal game rules. Candidate policy may inherit the selected base constraint; do not claim these tests were executed
- **Invalidation:** upstream change or owner adoption
- **Affected:** OD-11, MAP-042 §5 R02 note

### E27

- **Claim:** Import fixtures: SCAN rows IGU-360 unresolved 0,0% / WAM-436 Wormhole Unstable Wormhole 100,0%; assertions: unchanged → 0 created/changed; partial 42,5% → group set, 0 fully-scanned; decimal separators 100,0%/100.0%/100.0 % all fully scanned. Fixtures unexecuted here; not a CCP scan-format spec
- **Source:** S3 src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-114
- **Source report:** [MAP-047](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d23a249231ca47e97f38889c06da78bb5a8ff599/docs/map/specs/loop-map-047-wh-research.md)
- **Scope:** signature/mass/observation boundaries
- **Observed:** commit 2a493fad; no per-file retrieval timestamp supplied
- **Status:** inspected-source
- **Contradictions:** Upstream constraints/test fixtures are not authoritative universal game rules. Candidate policy may inherit the selected base constraint; do not claim these tests were executed
- **Invalidation:** test/behaviour change
- **Affected:** OD-11

### E28

- **Claim:** Pathfinder ConnectionModel: nominalLifespan Schema::DT_INT default null, no unit; JUMP_MASS_TYPES WhJumpMassS/M/L/Xl; JUMP_MASS_BUCKETS descending 1,000,000,000→Xl, 375,000,000→L, 62,000,000→M, 5,000→S (comment: matches init.js Init.wormholeSizes, not supplied); jumpMassTypeFromMass kg input; defaultMassFromEndpoints C13→small C1→medium, most restrictive wins; applyMassFromWormholeTypeId reads local Universe TypeModel, groupId == ESI_GROUP_WORMHOLE_ID (value not supplied); ConnectionLog shipMass logged. All are implementation constants, not authoritative CCP rules
- **Source:** S2 app/Model/Pathfinder/ConnectionModel.php complete 647 lines
- **Source report:** [MAP-047](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d23a249231ca47e97f38889c06da78bb5a8ff599/docs/map/specs/loop-map-047-wh-research.md)
- **Scope:** signature/mass/observation boundaries
- **Observed:** commit 06af7d86; no per-file retrieval timestamp supplied
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** upstream change
- **Affected:** OD-06, MAP-042 WH-F14

### E29

- **Claim:** WHSystemLink: EndOfLifeStatus Normal, Size Large, MassStatus Normal; JumpHistory collection (WHJumpLog class referenced, file absent)
- **Source:** S3 Models/Db/WHSystemLink.cs lines 1-48
- **Source report:** [MAP-047](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d23a249231ca47e97f38889c06da78bb5a8ff599/docs/map/specs/loop-map-047-wh-research.md)
- **Scope:** signature/mass/observation boundaries
- **Observed:** commit 2a493fad; no per-file retrieval timestamp supplied
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-06

### E30

- **Claim:** SDE access: static data changes only with game updates; latest at developers.eveonline.com/static-data/; JSON Lines or YAML; latest.jsonl record key sde gives build number; data zips eve-online-static-data-<build>-<variant>.zip; changes/<build>.jsonl; latest-jsonl.zip/latest-yaml.zip redirect; ETag/Last-Modified supported, non-static cached 5 minutes. No build number, zip or SDE content fetched
- **Source:** S1 docs/services/static-data/index.md lines 1-60
- **Source report:** [MAP-047](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d23a249231ca47e97f38889c06da78bb5a8ff599/docs/map/specs/loop-map-047-wh-research.md)
- **Scope:** signature/mass/observation boundaries
- **Observed:** commit 98b42d5; receipt sha256 e5ae49a7910c59c95d4075c5a5808658bd8f47c164b400bbc7197d8d423a75e1, etag "c1fd1e5af7d67ea4451079101b5b6596145a7ba02edb938a9132b6d37c964657"; no per-file retrieval timestamp supplied
- **Status:** documented-primary
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** esi-docs change
- **Affected:** OD-06, mass/life data sourcing

### E31

- **Claim:** WHJumpLog jump-evidence fields (pilot, ship, mass, jump date) pinned by MAP-042 §4 but absent from next-observations-sources.md
- **Source:** MAP-047 §2 absence note
- **Source report:** [MAP-047](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d23a249231ca47e97f38889c06da78bb5a8ff599/docs/map/specs/loop-map-047-wh-research.md)
- **Scope:** signature/mass/observation boundaries
- **Observed:** Not directly observed; synthesis/gap recorded in MAP-047 at d23a249231ca47e97f38889c06da78bb5a8ff599; no runtime measurement
- **Status:** unresolved
- **Contradictions:** This is a packet-local omission: earlier MAP-042 points to a pinned WHJumpLog source. It is not proof that the file or prior evidence does not exist
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-06, MAP-042 §5 R04

### E32

- **Claim:** Pathfinder: PHP 8.5 badge, composer >=8.2, ext-sodium; v3.0 breaking changes: DB schema v2 columns on system/connection/map/character + map_group table; ESI tokens plaintext → libsodium crypto_secretbox 32-byte hex key, fails closed if blank; SMTP removed; ini → env; WHITELIST → ALLOWLIST; PKCE default; deployment/migration/backup guidance in external pathfinder-containers, not supplied. README claims unverified
- **Source:** S2 README.md + composer.json
- **Source report:** [MAP-048](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d5299f396d5878ca6b436aa49dede05b11b4f8dd/docs/map/specs/loop-map-048-wh-research.md)
- **Scope:** fork/database options
- **Observed:** commit 06af7d86; README receipt sha256 1d7c461a1e06cb0425312d1380a34ff994632986f00728130e19c9196f9a1bd1; composer.json retrieved 2026-11-02T15:49:05.695523Z per MAP-045 packet; no README retrieval timestamp in MAP-048 packet
- **Status:** inspected-source
- **Contradictions:** No additional conflict identified within the supplied material; this does not constitute independent runtime verification
- **Invalidation:** newer commit
- **Affected:** OD-02, OD-12

### E33

- **Claim:** EVE-WHMapper: net10.0; EF Core/Npgsql 10.* → PostgreSQL assumption; docker-compose postgres:17-alpine named volume postgres:/data/postgres; redis:8-alpine network-only, no data volume; image ghcr.io/pfh59/eve-whmapper:latest; placeholder EveSSO__ClientId/Secret. README claims (multi-account, per-map access, auto ESI tracking, route planner, jump module, public instance whmapper.ovh) unverified
- **Source:** S3 WHMapper.csproj + deploy/docker/eve-whmapper/docker-compose.yml + README.md
- **Source report:** [MAP-048](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d5299f396d5878ca6b436aa49dede05b11b4f8dd/docs/map/specs/loop-map-048-wh-research.md)
- **Scope:** fork/database options
- **Observed:** commit 2a493fad; csproj retrieved 2026-11-02T15:49:06.542909Z per MAP-045 packet; README/docker-compose receipts given in MAP-048 packet, no retrieval timestamps
- **Status:** inspected-source
- **Contradictions:** PostgreSQL is evidenced for the WHMapper option; this does not name Pathfinder's engine or establish that any deployment/restore was tested
- **Invalidation:** newer commit or supplied lockfile
- **Affected:** OD-02, OD-12

### E34

- **Claim:** New implementation: zero code evidence; option C is unevidenced, not a demonstrated shortcut; borrowings (signature dedupe, per-map access, ESI SSO/PKCE, encrypted-token-at-rest pattern, map isolation) are suggestions only
- **Source:** MAP-048 §5 + MAP-042 §3/§11
- **Source report:** [MAP-048](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d5299f396d5878ca6b436aa49dede05b11b4f8dd/docs/map/specs/loop-map-048-wh-research.md)
- **Scope:** fork/database options
- **Observed:** Not directly observed; synthesis/gap recorded in MAP-048 at d5299f396d5878ca6b436aa49dede05b11b4f8dd; no runtime measurement
- **Status:** proposed
- **Contradictions:** Absence of new-implementation code does not establish that new code is cheaper or faster than extending an existing mapper
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-02

### E35

- **Claim:** Backup/restore: neither packet contains restore-test evidence, row-count comparison, import into empty DB, or credentials/grant non-leakage validation; backup creation distinct from restore verification (MAP-042 §5 R10, §9, §11)
- **Source:** MAP-048 §7 + MAP-042 §11
- **Source report:** [MAP-048](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d5299f396d5878ca6b436aa49dede05b11b4f8dd/docs/map/specs/loop-map-048-wh-research.md)
- **Scope:** fork/database options
- **Observed:** Not directly observed; synthesis/gap recorded in MAP-048 at d5299f396d5878ca6b436aa49dede05b11b4f8dd; no runtime measurement
- **Status:** unresolved
- **Contradictions:** Writing a restore plan or producing a backup/checksum does not supply executed restore evidence
- **Invalidation:** Reassess if the referenced upstream commit, metadata snapshot, implementation, owner decision or actual runtime evidence changes; scope remains this packet only
- **Affected:** OD-08

## 4. Contradictions reconciled

1. Access default: MAP-042 §5 R06 proposes explicit-grant-only as candidate default (OD-13 open). MAP-046 E23 shows upstream WHMapAccess permissive empty-list default flipping to explicit grants once rows exist. Neither is adopted; OD-13 remains an explicit owner decision before build acceptance.
2. Signature name length: MAP-042 OD-11 undecided; MAP-047 E26 upstream StringLength(7) is a reference constraint only, not adopted.
3. Revocation: MAP-042 §11 states "revocation via ESI revoke endpoint plus server-side invalidation, runtime-unverified." MAP-043 E06/E07 narrow this: provider revokes refresh token only, clears cache only on success; no access-token revocation path; revocation failure leaves cache intact.
4. Database engine: MAP-042 OD-12 undecided; MAP-048 E32 Pathfinder engine unnamed vs E33 WHMapper PostgreSQL evidenced. No conflict — different options; OD-12 remains open.
5. Stack: MAP-042 §11 options A (new implementation), B (Pathfinder fork), C (WHMapper fork); MAP-048 uses a different local A/B/C order; MAP-048 confirms none evidenced as build-ready; PHP and C# internals incompatible. OD-02 remains open.

No finding was silently dropped; no side was chosen.

## 5. Proposed amendments register (not mandates)

A-01 — Anchor MAP-042 §11 security/privacy with MAP-043 E06/E07: refresh-token-only revocation, ClearToken on success only, divergence on failure, no access-token revocation path evidenced. Affects MAP-042 §11, OD-07.
A-02 — Anchor OD-03 to MAP-044 E10–E14 scope/rate-limit/cache table as minimum-scope evidence pending owner scope selection. Affects OD-03, MAP-044 §5-8.
A-03 — Anchor OD-07 to MAP-043 E06 provider limits: in-memory cache only, no encryption-at-rest evidenced, revocation not confirmed. Affects OD-07, MAP-043 §4.
A-04 — Anchor OD-14 to MAP-043 E04/E08: consent player-controlled at SSO; scp/sub claims documented; defaults undecided. Affects OD-14, MAP-043 §3.4/§3.6.
A-05 — Keep OD-13 open: explicit-grant-only (MAP-042 proposal) vs upstream permissive empty-list default; enforce chosen rule by code not yet supplied. Affects OD-13, MAP-042 §5 R06, MAP-046 E23.
A-06 — OD-11: upstream 7-char Name constraint cited as reference only; candidate max-length undecided pending owner decision. Affects OD-11, MAP-042 §5 R02 note, MAP-047 E26.
A-07 — OD-12: Pathfinder unnamed vs WHMapper PostgreSQL; engine undecided. Affects OD-12, MAP-048 E32/E33.
A-08 — OD-02: MAP-042 options A (new implementation), B (Pathfinder fork), C (WHMapper fork); MAP-048 uses another local ordering; none build-ready evidenced. Affects OD-02, MAP-048 §10.
A-09 — OD-04: dependency licence/security audit for chosen manifest, incl. config.audit.ignore PKSA-y2cr-5h3j-g3ys review and composer.lock verification. Affects OD-04, MAP-045 E16-E18.
A-10 — OD-05: asset licences (favicon/logo, wh-effects.json), EVE game data/ESI terms, CCP developer agreement review. Affects OD-05, MAP-045 E19-E20.
A-11 — OD-08: restore-test evidence required (import into isolated instance, counts/references/permissions, cursor replay, no credential leakage); backup creation ≠ restore verification; no restore-test evidence exists. Affects OD-08, MAP-042 §5 R10, MAP-048 §7.
A-12 — Record E15 snapshot-limited negative: no character-scoped jump-log endpoint evidenced in ESI inventory; jump-log requirement unresolved pending owner decision or further upstream evidence. Affects OD-03, MAP-044 E15.
A-13 — Add OD-01 (concurrent-edit exception policy): optimistic revision conflict adopted as single rule; last-write-wins only as explicit owner exception with audit entry; affects WH-042-API-03, MAP-042 §7 and WH-F04. Status: unresolved owner decision carried from MAP-042 §15 item 1; not adopted as a mandate.

## 6. Residual owner decisions and runtime checks

OD-01 concurrent-edit exception policy (optimistic revision conflict as single rule; last-write-wins only as explicit owner exception with audit entry; affects WH-042-API-03, MAP-042 §7 and WH-F04); OD-02 stack/runtime (blocks B01 and all milestones); OD-03 ESI scopes/rate limits/issuer runtime contract (blocks opt-in tracking, export visibility); OD-04 dependency licence/security audit incl. audit-ignore (blocks copying decision); OD-05 asset/game-data/ESI/CCP agreement legal review; OD-06 stale threshold, mass-bucket adoption, route constraints (blocks route planner acceptance); OD-07 auth/token storage, encrypted-at-rest adoption, revocation effectiveness (blocks auth design); OD-08 restore-test evidence (blocks release recovery); OD-09 unseen handler implementations + per-handler authorization tests (blocks authorization acceptance); OD-10 bootstrap actor/initial owner designation (blocks API-13..16); OD-11 signature name max-length; OD-12 database engine; OD-13 access default; OD-14 opt-in default, sharing expiry, per-jump vs continuous.

Runtime checks pending the built app: import/export roundtrip; backup checksum vs test restore into empty database with row-count match; outage read-only/write-reject/queue drain; concurrent conflict surfaces both versions; per-handler authorization; ESI scopes/rate limits/issuer runtime verification; full dependency licence/security audit; asset licence checks; restore test into isolated instance.

## 7. Missing evidence (explicitly listed, never used as inputs)

- EVE-WHMapper WHJumpLog.cs lines 1-47 (pilot, ship, mass, jump-date fields) — absent from next-observations-sources.md despite MAP-042 §4 pin.
- ESI character-scoped jump-log or jump-history endpoint — not in snapshot inventory.
- Restore-test evidence for either database candidate.
- CCP developer agreement acceptance status and scope.
- Composer exact package versions/declarations are available in MAP-045's projection; individual licence texts and transitive legal compatibility are not verified. NuGet exact resolved lock/dependency licences remain unavailable.
- Asset licences (Pathfinder favicon/logo; WHMapper wh-effects.json).
- IEveMapperAccessHelper / IEveMapperUserManagementService implementations; handler registration; enforceable access query over WHMapAccess.
- First-instance seed / bootstrap actor mechanism.
- Cache invalidation layer on grant revocation, membership change, logout.
- Any authenticated ESI call, app registration, or accepted terms.

## 8. Historical native checks reported (text comparisons, not tool execution)

- Read all eight pinned packets at the revisions above; verified supplied receipt sha256 values where stated (compatibility-dates, openapi.json, oauth discovery, access-pack files, esi static-data index, composer.json, csproj).
- Cross-checked MAP-043 discovery metadata against documented endpoints (authorize, token, revoke, jwks, verify).
- Cross-checked MAP-047 signature constraints and import fixtures against MAP-042 OD-11 and WH-F03.
- Cross-checked MAP-046 access-default comment against MAP-042 §5 R06 / OD-13; flagged conflict (section 4 item 1).
- Separated declared vs locked dependency versions (PHP via unverified projection; .NET declarations only, no lock).
- Restricted E11 char-location group membership to location/online/ship; described corporationhistory separately as unauthenticated with no documented rate-limit group; kept derived ~600-call arithmetic labelled derived and confined to the three location-family operations.
- Replaced truncated ESI oauth-authorization-server receipt hash with exact 64-character value dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572 in all locations.
- Added OD-01 to section 6 with amendment A-13 citing WH-042-API-03, MAP-042 §7 and WH-F04.
- Did not: call any endpoint, register an app, accept terms, execute tests, choose a stack/database, infer handler security, treat documentation as implementation evidence, or use unaccepted drafts as requirements.

Limitations: all evidence is pinned to commits/snapshots above; unaccepted reports are source claims, not verified facts; evidence absent from this snapshot is unresolved; no runtime/security/compatibility/licence compliance claim is made.


## 9. Final coordinator reconciliation

The owner asked to finish this handoff. Controlled statuses and all mandatory fields are now supplied without inventing dates, contradictions, source measurements or runtime success. Missing observations explicitly say not observed. Three public HTTP metadata snapshot hashes were independently recomputed from the saved original bytes; six published reports matched the exact local copies. Option labels are scoped by report to avoid an A/B/C mix-up. MAP-048's missing-Composer-lock claim applies to its own input packet, not the whole research batch. E31's missing WHJumpLog evidence is also packet-local, not global.

No fresh native critique, project acceptance, app implementation, server access or owner-choice approval occurred. This finishes the research register; later blueprint amendments must cite these records and remain labelled source fact versus proposed design.
