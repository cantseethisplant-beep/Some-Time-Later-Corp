# MAP-038 — WH Identity, Access, Privacy and Threat Model

**Task:** MAP-038 · **Claim commit:** d8dbd912b64879dcf792f7265387f721d66586bb · **Worker:** hermes-laptop-map-038-auto-20261030 · **Input revision:** 849978908daabe3d2a45f0e758625eedc4bdde30 · **Output path:** docs/map/specs/loop-map-038-wh-design.md

## Status of this document

Proposed design draft. Not accepted, not merged, not build-ready. Baseline intent comes from docs/map/WH-FIRST-BRIEF.md at input revision 84997890; older hosting-manager scope is optional background only and is not part of the mapper core. All upstream facts cite pinned extracts at commits 06af7d86fe6456947fb960220c54d02a8623c0ff (Pathfinder) and 2a493fad9acec9a8e15b619f7943ae8b6e7f30da (EVE-WHMapper). No runtime verification, licence audit, dependency audit or security audit has been performed.

## 1. Baseline intent versus proposed schema rules

Baseline (owner direction, WH-FIRST-BRIEF): the app is a wormhole mapping/intel/operations tool; cloud hosting is an added supporting capability. Proposed MVP data concerns include: shared connection chain map; probe-signature paste/import/edit/history; timestamps and stale observations; observed hole life/size/mass and jump evidence; route planning over mapped connections; per-map permissions; opt-in pilot/location tracking; basic notes and observed intel; corporation administration; backup/export/import; release recovery. Location observations, jump logs, mass estimates and user intel must retain source/time/uncertainty. The tool must not promise complete hostile detection, guaranteed safe routes, exact remaining mass, perfect location polling or knowledge of unobserved activity.

Everything in sections 3–18 is a proposed schema/design rule, not an accepted requirement. An unresolved policy marked in this document must not become a mandate in examples or tests.

## 2. Evidence index and citation convention

Citations use the form [source, commit, path, lines]. Supplied extracts:

- [WH-FIRST-BRIEF, 84997890, docs/map/WH-FIRST-BRIEF.md]: owner direction.
- [pf-sources, 06af7d86, docs/map/research/pf-sources.md]: Pathfinder LICENSE (MIT, lines 1–22); README (lines 1–61); composer.json (lines 1–81); ConnectionModel.php (lines 1–160); SystemSignatureModel.php (lines 1–160); MapModel.php (lines 1–160).
- [wh-sources, 2a493fa, docs/map/research/wh-sources.md]: EVE-WHMapper LICENSE (MIT, lines 1–22); README (lines 1–60); WHMapper.csproj (lines 1–52); WHSignature.cs (lines 1–113); WHMapAccess.cs (lines 1–48); WHMapperContext.cs (lines 1–104); deploy/docker/eve-whmapper/docker-compose.yml (lines 1–46); WHSystemLink.cs (lines 1–49); WHJumpLog.cs (lines 1–47); EVEOnlineAuthenticationDefaults.cs (lines 1–43); WHSignatureHelperImportTests.cs (lines 1–115).

Both root licences are MIT; substantial reuse must keep copyright and permission notices. Assets, dependencies and game data require separate checks before any copying.

## 3. Proposed login and account linking

Proposed: EVE CCP SSO as the identity provider, compared against upstream behavior rather than adopted blindly. EVE-WHMapper inspects the authorize/token/JWKS/revoke endpoints at https://login.eveonline.com/..., default scheme "EVEOnline", callback /signin-eveonline, issuer "https://login.eveonline.com" and audience "EVE Online" [wh-sources, 2a493fa, src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs, lines 1–43]. Pathfinder enables PKCE on CCP SSO by default, gates /setup behind PF_SETUP_ENABLED, and activates production guards under APP_ENV=production [pf-sources, 06af7d86, README, lines 1–61, security hardening section].

Proposed decisions (unaccepted):

- One EVE character links to one local user account; a person may link multiple characters as separate account subjects.
- External identity binding = character ID + issuer. This is a purely proposed local decision, not an upstream default. The cited EVE-WHMapper OAuth defaults extract contains only endpoints, scheme, callback path, issuer and audience; it contains no character-ID identity claim [wh-sources, 2a493fa, src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs, lines 1–43]. ESI scopes, rate limits and the issuer runtime contract are unspecified and pending owner and upstream verification; none are invented here.
- Linking requires explicit user consent; no silent account creation from ESI claims.

## 4. Roles, permissions and negative permission cases

Proposed role set: instance host/administrator, corporation-level grantee, character-level grantee, per-map grantee. Upstream comparison: WHMapAccess stores one access entry per map/entity (character/corporation/alliance) with GrantedAt, and documents that "when no access entries exist for a map, all instance members can access it. When at least one access entry exists, only explicitly granted entities can access it" [wh-sources, 2a493fa, src/WHMapper/Models/Db/WHMapAccess.cs, lines 1–48]. Pathfinder MapModel exposes editable map fields including allowGroups (default 1), logActivity (default 1) and logHistory (default 0) [pf-sources, 06af7d86, app/Model/Pathfinder/MapModel.php, lines 1–160].

Proposed rule: maps start with no access entries; the stricter explicit-grant-only behavior is the candidate default, and the permissive "all instance members" behavior is an optional owner override, not adopted by default. Negative permission cases that must be denied:

- Unauthenticated requests to any map read, write or event.
- A character with no access entry on a map that has at least one access entry.
- A revoked or unlinked character.
- A character whose corporation or alliance membership has lapsed, until revalidated (stale membership, section 15).

## 5. Opt-in location/jump sharing

Proposed: location and jump sharing is opt-in per character. EVE-WHMapper README claims automatic location tracking via ESI and pilot tracking as core features [wh-sources, 2a493fa, README, lines 1–60]; these are README claims, not verified behavior. Proposed: no automatic tracking without explicit opt-in; sharing grants expire; one character's location is never shared with another character's account without separate consent; jump logs record CharacterId and JumpDate [wh-sources, 2a493fa, src/WHMapper/Models/Db/WHJumpLog.cs, lines 1–47] and must retain source/time/uncertainty per the brief.

Unresolved: default opt-in state, expiry length, and whether sharing is per-jump or continuous.

## 6. Timestamps and observation uncertainty

All observations must retain source/time/uncertainty [WH-FIRST-BRIEF]. Upstream patterns to compare: Created/Updated DateTime UTC plus CreatedBy/UpdatedBy on WHSignature [wh-sources, 2a493fa, src/WHMapper/Models/Db/WHSignature.cs, lines 1–113]; JumpDate set to DateTime.UtcNow on WHJumpLog [wh-sources, 2a493fa, src/WHMapper/Models/Db/WHJumpLog.cs, lines 1–47]; eolUpdated and nominalLifespan on connections [pf-sources, 06af7d86, app/Model/Pathfinder/ConnectionModel.php, lines 1–160].

Proposed: store all timestamps in ISO-8601 UTC; record observer, source system and uncertainty for every mass/life/jump observation; never treat a timestamp as proof of current presence. Unresolved: uncertainty units and precision.

## 7. Token storage, rotation and revocation

Proposed: tokens are server-side only and never emitted to clients. Pathfinder encrypts ESI tokens at rest with libsodium crypto_secretbox using a 32-byte hex key and fails closed if blank [pf-sources, 06af7d86, README, lines 1–61, security hardening]; WebSocket tokens are HMAC-bound to the PHP session, require WS_TOKEN_SECRET, and enforce production origin checks [same source]. EVE-WHMapper documents a revoke token endpoint [wh-sources, 2a493fa, EVEOnlineAuthenticationDefaults.cs, lines 1–43].

Proposed decisions: encrypt at rest with a configured key; fail closed if the key is missing; rotate tokens on compromise suspicion or on an owner-defined schedule (interval unresolved); revoke by calling the ESI revoke endpoint plus server-side invalidation; check a revocation list before each privileged operation. Revocation effectiveness and ESI rate limits are unverified.

## 8. Minimum-scope discovery prerequisites

Proposed: no ESI discovery or data import occurs without an explicit, current user grant; only minimum scopes are requested; the scope list is pending upstream verification and is intentionally empty in this document. Prerequisite check before any upstream call: valid unrevoked token plus consent plus required scope confirmed.

## 9. Unlink, delete and export

Backup creation and restore verification are distinct and must never be conflated; neither is designed here beyond the decision points below.

Proposed:

- Unlink character: revoke token, delete stored tokens and sessions, retain audit records (activity log must not be cascade-deleted when maps/systems are deleted [wh-sources, 2a493fa, WHMapperContext.cs, lines 1–104]).
- Delete map or personal data: cascade map-owned data per the upstream model pattern [wh-sources, 2a493fa, WHMapperContext.cs, lines 1–104]; audit history retained.
- Export: user-initiated JSON export of that user's own observations and links; game data and assets excluded pending separate licence checks.

Unresolved: export format version, deletion grace period, hard-delete versus soft-delete.

## 10. Audit retention

Proposed: append-only activity log with activity types keyed by explicit codes so they match across deployments [wh-sources, 2a493fa, WHMapperContext.cs, lines 1–104, activity seed data]. Retention period is an unresolved owner decision; no automatic deletion is proposed or mandated. Host/administrator access to audit logs is itself logged.

## 11. Server-side auth for reads/writes/events

Proposed: every read, write and socket event is authorized server-side against tenant (instance/map) context; clients are never trusted for authorization. Tenant isolation follows the upstream multi-tenant table layout (Instances, InstanceAdmins, InstanceAccesses, WHMaps scoped by WHMapId with cascade) [wh-sources, 2a493fa, WHMapperContext.cs, lines 1–104]. Unseen handlers are not claimed secure; authorization must be implemented and tested per handler.

## 12. Malicious imports

Proposed: signature imports are validated before persistence. Upstream tests show unresolved versus wormhole signatures, name length limits (StringLength 7), group/type resolution, and that only fully scanned (100%) signatures count as created [wh-sources, 2a493fa, src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs, lines 1–115; WHSignature.cs, lines 1–113]. Proposed checks: reject malformed scans; reject names exceeding length; reject unknown groups pending review; deduplicate by name+group+type ignoring audit fields (HasSameContent pattern). Import errors must not grant map access.

## 13. Session and socket replay

Proposed: short-lived sessions; socket tokens HMAC-bound to sessions with origin checks [Pathfinder README]; each socket event carries a timestamp and nonce; the server maintains a short replay cache (window unresolved). Replayed or post-session events are denied.

## 14. Cache leakage

Proposed: cache keys are namespaced by instance and map ID; caches are invalidated on unlink, revocation and membership change; no cross-tenant cache sharing. Redis appears in upstream docker-compose as an example cache backend [wh-sources, 2a493fa, deploy/docker/eve-whmapper/docker-compose.yml, lines 1–46]; its use is optional, not mandated.

## 15. Stale memberships

Proposed: corporation/alliance access entries are revalidated at login and on a periodic schedule (interval unresolved); a character that leaves a corporation does not retain map access through a stale corp entry until revalidation denies it. This is a proposed policy, not implemented behavior.

## 16. Administrator and host authority

Proposed: the instance host administers the instance; administrators manage access lists and instance settings. Administrator actions are audit-logged and do not bypass authorization for maps they are not granted on. Host authority is instance-level, not a blanket bypass of per-map or per-character denial.

## 17. Misuse cases and future tests (WH-SEC01 onward)

These are proposed future tests, not implemented or accepted. Each lists setup, input, expected denial and evidence needed.

- WH-SEC01 — Unauthenticated map read. Setup: fresh server, no session. Input: GET map/{id}. Expected denial: 401/403 before any data access. Evidence needed: route-protection test covering all read endpoints.
- WH-SEC02 — Deny-by-default on access-controlled map. Setup: map M has one access entry for corporation C1; character X belongs to C2. Input: X reads map M. Expected denial: 403. Evidence needed: access-list enforcement test comparing empty-list versus entry-exists behavior.
- WH-SEC03 — Revoked token still accepted. Setup: token T revoked via the ESI revoke endpoint. Input: API call bearing T. Expected denial: 401. Evidence needed: revocation-list check implementation and ESI revoke call log.
- WH-SEC04 — Socket replay after session end. Setup: capture socket event E under session S; end S. Input: replay E. Expected denial: invalid session or nonce. Evidence needed: WS token binding and replay-cache test.
- WH-SEC05 — Malicious signature import. Setup: scan row with name longer than 7 chars or invalid group. Input: ImportScanResult call. Expected denial/rejection: import rejected, audit recorded, no map change. Evidence needed: import validation test against WHSignatureHelperImportTests patterns.
- WH-SEC06 — Cross-tenant cache leakage. Setup: tenant A data cached under key K; tenant B requests K. Expected denial: tenant B receives no tenant A data. Evidence needed: cache-key namespace test.
- WH-SEC07 — Stale membership retention. Setup: character leaves corporation C; corp access entry still exists. Input: next login read attempt. Expected denial until revalidation. Evidence needed: revalidation hook test (policy timing unresolved).
- WH-SEC08 — Admin export bypass. Setup: administrator A requests export for a character not in A's maps. Expected denial: scope-bound export refusal. Evidence needed: export scope test.

## 18. Residual blockers and open decisions

- ESI scopes, rate limits and issuer contract are unknown; this document deliberately specifies none.
- No licence/dependency/security audit, runtime verification or security certification exists for either upstream project; MIT notices are retained only if substantial source is reused.
- Stack choice (maintained Pathfinder fork, separate integration, new implementation) is not decided; PHP and C# internals must not be combined by assertion.
- Owner decisions pending: opt-in defaults, sharing expiry, token rotation interval, audit retention period, deletion grace period, cache backend.
- Missing evidence: unseen handler implementations, ESI behavior at runtime, restore/verification procedures for backups.

This completes the scoped design draft. All items remain proposals pending independent acceptance.
