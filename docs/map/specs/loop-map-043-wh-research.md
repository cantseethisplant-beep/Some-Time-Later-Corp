# MAP-043 — SSO, token validation and revocation evidence

**Task:** MAP-043 — Research SSO, token validation and revocation evidence  
**Claim worker:** hermes-laptop-map-043-auto-20261030  
**Claim commit:** 398d68d456d6b3691565c1c394d894e187c60f2f  
**Input revision:** 6e023274d7cb692f36b132d980d5a335d4387897  
**Output path:** docs/map/specs/loop-map-043-wh-research.md  
**Status:** research report — not accepted, not merged, not build-ready, no implementation claimed  
**Loop:** WH research v1, cycle 201, research step 1

## 1. Purpose and evidence limits

This report is the MAP-043 deliverable: a source-linked research record of the EVE SSO/OAuth 2.0 authorization contract, JWT validation, token refresh and revocation, and the inspected upstream token-provider implementation. It is produced only from the pinned primary-source packets supplied for this task. No network, shell, account, delegation or server tool was used; no authenticated route was called, no app was registered, no terms were accepted, and no handler security was inferred.

The completed MAP-042 blueprint (commit 6e023274...) is context only: an unaccepted candidate, not a baseline to overwrite. Owner choices (stack, consent defaults, scopes) remain unresolved. Every finding is labelled documented-primary (pinned vendor text), inspected-source (public code read), public-metadata (snapshot), proposed (this report's framing), or unresolved (owner decision or missing evidence). Nothing certifies security, compatibility, licence acceptance, or runtime behavior.

## 2. Source inventory and pins

| Source | Commit / revision | Path | Receipt sha256 | Retrieved | Evidence type |
|---|---|---|---|---|---|
| esi/esi-docs | 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d | docs/services/sso/index.md | ea4b18924377dce47605cba1b2b2cefcf7979db55ca893b7b2c3e5a9af0e5213 | 2026-11-02T15:49:02Z | documented-primary, complete file lines 1-221 |
| esi/esi-docs | same | snippets/sso/authorization-code-pkce.py | 4e0ee19f660990b7fcafb8cff1313a245d4cb67411e5a2ad10ca04befda0b8a1 | 2026-11-02T15:49:03Z | documented-primary, complete file lines 1-71 |
| esi/esi-docs | same | snippets/sso/validate-jwt-token.py | c6a587cdcbb9a8dd8230835af7c4b67001c5bee1190dc2c11203b12f396362f6 | 2026-11-02T15:49:03Z | documented-primary, complete file lines 1-86 |
| pfh59/eve-whmapper | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | src/WHMapper/Services/EveOAuthProvider/Services/EVEOnlineTokenProvider.cs | cd98936057e5bed92b89fb629d80c69339ebed311b88aa8c5244cbd8239ed31c | 2026-11-02T15:49:03Z | inspected-source, complete file lines 1-162 |
| ESI public metadata | live snapshot | meta/compatibility-dates, meta/openapi.json, .well-known/oauth-authorization-server | 7ac78423..., 9a9a0f4..., dc04adbd... | 2026-11-02T15:49:01Z | public metadata snapshot, not runtime verification |
| Owner research policy | 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec | docs/map/research/LOCAL-RESEARCH.md | — | — | policy constraint |
| MAP-042 blueprint context | 6e023274d7cb692f36b132d980d5a335d4387897 | docs/map/specs/loop-map-042-wh-design.md | — | — | unaccepted baseline context only |

MIT root licence notices are reproduced where material is quoted (esi-docs CCP hf. 2015; eve-whmapper pfh59 2023); root MIT notices do not settle transitive dependencies, assets, game data, or the separate CCP developer agreement, which still requires owner review.

## 3. Documented EVE SSO / OAuth 2.0 contract (esi-docs)

All claims in this section come from esi-docs commit 98b42d5..., supplied lines as noted; they are documented vendor descriptions, not observed runtime behavior.

### 3.1 Registration and prerequisites
Before using SSO, developers register the application with the EVE Online Developers Portal, generating a client ID and secret. The client ID is public; the secret must be kept private. Applications may only request scopes assigned at registration, and redirect URLs must match registered URLs; any other URL is rejected. (index.md, Terms and important notes.)

### 3.2 Authorization Code flow
For web apps that can store the client secret server-side. The app builds a query string with response_type=code, client_id, redirect_uri, scope (space-separated), state (random CSRF nonce), redirects the user to the authorization_endpoint; after login and explicit consent, SSO redirects back with an authorization code and state; the app verifies state, then POSTs to the token_endpoint with grant_type=authorization_code and code, authenticated with Basic auth using client ID and secret. SSO responds with an access token and refresh token; the app verifies the access token. The authorization code is one-time and short-lived. (index.md Authorization Code.)

### 3.3 Authorization Code with PKCE
Enhanced flow for apps that cannot store a client secret; the snippet states "we do not use the client secret in this flow". The app generates a 32-byte random code verifier, base64url-encoded; code challenge = base64url(sha256(verifier)) without padding (RFC 4648). The authorization request adds code_challenge and code_challenge_method=S256. The token request body is grant_type=authorization_code, code, code_verifier, client_id (no secret). Endpoints: https://login.eveonline.com/v2/oauth/authorize and https://login.eveonline.com/v2/oauth/token. (snippet authorization-code-pkce.py lines 1-71; index.md PKCE section.)

### 3.4 Token exchange and token lifetimes
Access token: time-limited, valid only for the consented character and scopes, until expiry. Refresh token: long-lived, used to obtain new access tokens when the current one expires; usable indefinitely while the user has not revoked the application's access; must be kept secure. (index.md Terms.)

### 3.5 JWT validation
The access token is a JWT signed by EVE SSO with an RSA key. Validation: fetch metadata from https://login.eveonline.com/.well-known/oauth-authorization-server, read jwks_uri, fetch JWKS, match key by kid and alg from the token header, verify signature; check iss matches the SSO issuer (https://login.eveonline.com/, with login.eveonline.com also accepted); check aud is an array containing client_id and "EVE Online"; check exp Unix timestamp (not expired). Expired tokens are replaced via the refresh token. jose-compatible libraries may check exp automatically with an optional grace period. The validation snippet caches metadata for 300 seconds. (index.md Validating JWT Tokens; validate-jwt-token.py lines 1-86.)

### 3.6 JWT claims
sub = CHARACTER:EVE:<character-id>; name = character name; scp = array of granted scopes. (index.md JWT Token Claims.)

### 3.7 Revocation and discovery
Players can revoke access at any time (index.md How it works). The OAuth discovery metadata publishes revocation_endpoint = https://login.eveonline.com/v2/oauth/revoke, with revocation auth methods client_secret_basic, client_secret_post, client_secret_jwt; token endpoint auth methods the same; code_challenge_methods_supported = [S256]; id_token_signing_alg_values_supported = [HS256]; token_endpoint_auth_signing_alg_values_supported = [HS256]; response_types [code, token]; subject_types [public]; issuer https://login.eveonline.com; userinfo_endpoint https://login.eveonline.com/v2/oauth/verify. Applications should fetch endpoint URLs from the well-known metadata endpoint each time needed; URLs may change; caching for a reasonable time is safe and recommended. (metadata snapshot, oauth_discovery block; index.md Terms/Endpoints.)

## 4. Observed upstream token-provider code (EVE-WHMapper)

Source: pfh59/eve-whmapper commit 2a493fad..., src/WHMapper/Services/EveOAuthProvider/Services/EVEOnlineTokenProvider.cs, complete file lines 1-162, MIT-licensed (root notice retained). Class EveOnlineTokenProvider implements IEveOnlineTokenProvider. Inspected source code only: read once, not executed, not tested, not adopted as a pattern for this blueprint.

### 4.1 Token cache
In-memory only: ConcurrentDictionary<string, UserToken> _tokens keyed by AccountId, plus per-account SemaphoreSlim refresh locks. SaveToken requires non-null AccountId and upserts. GetToken returns the cached token; with autoRefreshed=true it refreshes first when expired. ClearToken removes the entry. No persistence, database, encryption-at-rest, or distributed-cache behavior is evidenced in this file.

### 4.2 Expiry check
IsTokenExpire treats null/default/DateTime.MinValue expiry as expired, and considers a token expired when DateTimeOffset.UtcNow > token.Expiry.AddMinutes(-5) — a 5-minute clock-skew margin before the recorded expiry.

### 4.3 Refresh rotation
RefreshAccessToken takes a per-account semaphore, double-checks expiry after waiting, throws InvalidOperationException("Refresh token is missing.") when the refresh token is empty, POSTs grant_type=refresh_token&refresh_token=<escaped> to _options.TokenEndpoint with Basic auth ClientId:ClientSecret, requires success (EnsureSuccessStatusCode), deserializes EveToken, then sets AccessToken, RefreshToken (may rotate), and Expiry = UtcNow.AddSeconds(ExpiresIn).UtcDateTime, and saves the token. Failure modes: missing refresh token; non-success HTTP response (exception propagates, old token remains); null deserialized token (NullReferenceException). Concurrency is serialized per account by the semaphore.

### 4.4 Revocation
RevokeToken gets the cached token, throws on missing refresh token, POSTs token_type_hint=refresh_token&token=<escaped> to _options.RevokeTokenEndpoint with Basic auth ClientId:ClientSecret. On non-success it deserializes ErrorResponse (error_description) and throws ArgumentException; on success it calls ClearToken(accountId). Failure modes: missing token; revocation HTTP error — local token is NOT cleared, so remote revocation and local cache can diverge; deserialization error — token not cleared. No access-token revocation path is present; only refresh-token revocation with token_type_hint=refresh_token is observed.

### 4.5 Failure-case register

| Case | Observed code behavior | Local/remote divergence | Status |
|---|---|---|---|
| Refresh token missing | InvalidOperationException before any HTTP call | none | inspected |
| Refresh endpoint non-success | exception; old token remains in cache | remote may have rotated; local stale | inspected |
| Refresh deserialization null | NullReferenceException | none | inspected |
| Revoke endpoint non-success | ArgumentException; ClearToken NOT called | remote may have revoked; local cache holds token | inspected — external revocation ≠ guaranteed local logout |
| Revoke deserialization error | exception propagates; token not cleared | divergence possible | inspected |
| Concurrent refresh per account | semaphore serializes; second waiter sees fresh token | none | inspected |

## 5. Public discovery / ESI metadata contract (snapshot)

Snapshot retrieved 2026-11-02T15:49:01Z; compatibility_date_requested 2026-08-18; spec version 2026-08-18; title "EVE SKINR Ingenuity (ESI) - tranquility". Receipts: compatibility-dates sha256 7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299 (208 bytes); openapi.json sha256 9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6 (614,672 bytes); well-known sha256 dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572 (813 bytes). License: EVE Developer License (https://developers.eveonline.com/license-agreement); terms of service linked. No agreement was accepted.

| Item | Value | Source | Status |
|---|---|---|---|
| issuer | https://login.eveonline.com | oauth_discovery | public metadata |
| authorization_endpoint | https://login.eveonline.com/v2/oauth/authorize | oauth_discovery | public metadata |
| token_endpoint | https://login.eveonline.com/v2/oauth/token | oauth_discovery / snippet | public metadata + documented sample |
| revocation_endpoint | https://login.eveonline.com/v2/oauth/revoke | oauth_discovery | public metadata |
| jwks_uri | https://login.eveonline.com/oauth/jwks | oauth_discovery | public metadata |
| userinfo_endpoint | https://login.eveonline.com/v2/oauth/verify | oauth_discovery | public metadata |
| code challenge methods | S256 only | oauth_discovery | public metadata |
| token auth methods | client_secret_basic, client_secret_post, client_secret_jwt | oauth_discovery | public metadata |
| id token signing algs | HS256 | oauth_discovery | public metadata |
| Relevant scoped paths | characters/location (esi-location.read_location.v1), online (esi-location.read_online.v1), ship (esi-location.read_ship_type.v1); rate-limit group char-location 1200 tokens / 15m; cache event-based or ttl-based, 5–60 s | openapi selected_paths | public metadata schema |

Absence from this path inventory is not proof of absence from all CCP services. Revalidate against the selected compatibility date before implementation. No authenticated route was called.

## 6. Claim validation register

| # | Claim | Source | Evidence type | Validity / version | Invalidated by | Status |
|---|---|---|---|---|---|---|
| C1 | SSO is OAuth 2.0; scopes are user-consented permissions | esi-docs index.md | documented-primary | pinned commit 98b42d5 | vendor doc change | documented |
| C2 | PKCE: S256 challenge; verifier 32 bytes base64url; no client secret | snippet pkce.py | documented-primary | pinned commit | vendor doc change | documented |
| C3 | JWT: RSA-signed; verify via JWKS from metadata; iss, aud (client_id + "EVE Online"), exp | index.md + validate-jwt-token.py | documented-primary + inspected snippet | pinned commit | vendor doc / key change | documented |
| C4 | Refresh token long-lived; revocable by user at any time | index.md Terms | documented-primary | pinned commit | vendor policy change | documented |
| C5 | Revocation endpoint exists; auth methods include client_secret_basic/post/jwt | metadata oauth_discovery | public metadata snapshot | snapshot 2026-11-02 | endpoint rotation | observed-metadata, not called |
| C6 | EVE-WHMapper provider refreshes via refresh_token grant with Basic auth; 5-minute expiry skew; revokes refresh token and clears cache on success | EVEOnlineTokenProvider.cs | inspected-source | commit 2a493fad | upstream code change | inspected |
| C7 | Revocation failure leaves local cache intact (ClearToken only on success) | EVEOnlineTokenProvider.cs | inspected-source | commit 2a493fad | upstream code change | inspected |
| C8 | Location/ship/online ESI paths require listed OAuth scopes; rate limits apply | openapi selected_paths | public metadata | compatibility date 2026-08-18 | date/version change | observed-metadata |

## 7. Rotation and revocation failure cases (derived)

- Access-token expiry is handled by refresh rotation; refresh failure leaves the caller without a usable access token until a new authorization grant is obtained (no re-auth path exists in the provider code).
- Refresh-token revocation at the SSO does not by itself clear local caches; the provider clears only after a successful revocation call. A failed revocation leaves local and remote state divergent.
- Revoking the refresh token invalidates future rotation; the current access token remains valid until its own expiry unless separately invalidated (no access-token revocation path is evidenced).
- Clock skew: tokens are treated expired 5 minutes before Expiry; skewed clocks may trigger early refresh or validation failure.
- Metadata or endpoint changes (jwks_uri, revocation_endpoint) invalidate cached discovery values; the docs recommend per-use fetch with reasonable caching.

## 8. Distinctions that must not be collapsed

1. External token revocation (SSO revoke endpoint against a refresh token) is distinct from local session/cache logout (ClearToken dropping the in-memory entry). The provider does the latter only after the former succeeds; a revocation failure leaves divergence.
2. Both are distinct from consent revocation by the player at the SSO/account level, which the docs describe as player-controlled at any time; no consent-status API is evidenced in these packets.
3. Access-token expiry is distinct from refresh-token revocation: an expired access token can be rotated; a revoked refresh token cannot.
4. Documented contract (vendor text/metadata) is distinct from inspected provider behavior; neither is runtime evidence for this project.

## 9. Minimum-scope questions (unresolved; owner decisions)

These are questions, not mandates. No consent defaults are chosen here.
- Q1 (OD-03): Which ESI scopes are in scope for this WH tool (e.g., location, ship, online, corporation membership), what are their rate limits, and what is the issuer/audience contract at runtime? Blocks consent workflow and export visibility.
- Q2 (OD-07): How are tokens stored server-side (encrypted at rest?), how is revocation effectiveness confirmed, and what happens on key loss? Blocks auth design.
- Q3 (OD-14): Opt-in default state, sharing expiry, per-jump vs continuous tracking; who grants consent and how is it revoked locally? Blocks R07 tracking.
- Q4: Which token lifecycle events (refresh failure, revocation failure) trigger local session invalidation in this implementation? Not answered by the packets.
- Q5: Does the application register a client and accept the CCP developer agreement? Not performed here; requires owner action outside this task.

Invalidation triggers: upstream endpoint/auth-method changes, compatibility-date changes, CCP agreement changes, observed runtime behavior contradicting documentation.

## 10. Blueprint passages needing proposed amendments

MAP-042 (unaccepted context) section 11 states "revocation via ESI revoke endpoint plus server-side invalidation, runtime-unverified" and treats the encrypted-at-rest pattern as reference only. OD-03/OD-07/OD-14 remain open. This report's findings (§3–§7) should be cited in those passages rather than treated as adopted implementation. No blueprint text is changed by this report; amendments are proposed for the register handoff:
- Align §11 security/privacy with the revocation divergence finding (C7) and the no-access-token-revocation observation.
- Anchor OD-03 to the metadata scope/rate-limit table (§5) as minimum-scope evidence, pending owner scope selection.
- Anchor OD-07 to §4 (inspected provider limits: in-memory cache, no encryption evidenced, no revocation-confirmation behavior).
- Anchor OD-14 to §3.4/§3.6 (consent is player-controlled; claims scp/sub) as documented boundaries, with defaults undecided.

## 11. Missing evidence (report unavailable rather than invent)

- Runtime calls to authorize/token/revoke endpoints; no valid client credentials exist in this task.
- ESI runtime behavior: issuer/audience enforcement, exp grace periods, rate-limit headers, revocation responses for access vs refresh tokens.
- Token storage: encryption at rest, persistence, cache invalidation on consent change; none evidenced in the inspected provider.
- CCP developer agreement / EVE Developer License acceptance status and scope cost; root MIT notices do not cover it.
- Transitive dependency licences (composer.json, csproj), asset licences, EVE game data terms.
- Any player data, corporation data, or ISK/commercial model.
- Local session mechanics beyond the inspected in-memory provider (cookies, browser cache, sign-out UI).

## 12. Checks actually performed

- Read all pinned packets at the revisions above; verified supplied receipt sha256 values where stated.
- Cross-checked discovery metadata against documented endpoints (authorize, token, revoke, jwks, verify, well-known).
- Checked the inspected provider for refresh, expiry, revocation, and cache-clear behavior and enumerated its failure modes.
- Checked MAP-042 §11 and OD-03/07/14 for consistency with the sourced contract; found them marked runtime-unverified/unresolved, consistent with this report.
- Did not: call any endpoint, register an app, accept terms, execute tests, infer handler security, choose consent defaults, or treat documentation as implementation evidence.

