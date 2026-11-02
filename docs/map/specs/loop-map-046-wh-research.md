# MAP-046 — Research: map access, bootstrap and membership behavior

**Task:** MAP-046 — Research map access, bootstrap and membership behavior  
**Claim worker:** hermes-laptop-map-046-auto-20261030  
**Claim commit:** 1f2915de0262953dbdf7a92d9fb7af2c5894e22f  
**Output path:** docs/map/specs/loop-map-046-wh-research.md  
**Status:** research report — not accepted, not merged, not build-ready, no implementation claimed  
**Research version:** 1, loop policy: 1, loop kind: wh-research

## 1. Purpose and evidence limits

This report is the MAP-046 deliverable: a source-linked research report on map access, first-owner bootstrap, and membership behavior for the WH-first blueprint candidate (MAP-042, commit 6e023274d7cb692f36b132d980d5a335d4387897). It is produced solely from pinned public primary-source snapshots supplied by the local guarded reader. No network, shell, account, delegation, or server tools exist in this session; reading the packets is the only research performed. No upstream test was executed, no player data accessed, and no implementation exists.

Evidence status labels used below: documented-primary (pinned source text), inspected (file read in full), proposed (this report's recommendations), unresolved (owner decision or missing evidence). A receipt hash proves a file was fetched, not that it is secure or correct. The root MIT licence notice in the access pack does not settle transitive dependencies, assets, EVE game data, ESI terms, or the separate CCP developer agreement. The MAP-042 blueprint is quoted context only; nothing here accepts it or overrides owner choices.

## 2. Source inventory

| Source | Revision | Role |
|---|---|---|
| docs/map/specs/loop-map-042-wh-design.md | 6e023274d7cb692f36b132d980d5a335d4387897 | Baseline WH blueprint candidate; unaccepted context |
| docs/map/research/LOCAL-RESEARCH.md | 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec | Local research policy and inventory |
| docs/map/research/NEXT-SOURCE-SNAPSHOT.json | 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec | Snapshot inventory; pins esi/esi-docs 98b42d5..., pathfinder 06af7d8..., eve-whmapper 2a493fa... |
| docs/map/research/next-access-sources.md | 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec | Fresh pinned access primary-source pack |

Access pack files (all pfh59/eve-whmapper @ 2a493fad9acec9a8e15b619f7943ae8b6e7f30da, supplied as complete files, retrieved 2026-11-02 between 15:49:07 and 15:49:09 UTC):

| File | Receipt sha256 | Bytes | Lines supplied |
|---|---|---|---|
| Services/EveMapper/AuthorizationPolicies/EveMapperRequirementHandlerBase.cs | 145ecb77a06c7a9ea1e7447d217bc521db75145b310b66164da0aa0d5c5b2436 | 3023 | 1-65 (complete) |
| Services/EveMapper/AuthorizationPolicies/EveMapperAccessHandler.cs | 6b5b80bce4bc832491bcf3d2a6425ab6900ce0af80ca1753d8b01c749773e683 | 838 | 1-21 (complete) |
| Services/EveMapper/AuthorizationPolicies/EveMapperAdminHandler.cs | cf80b3835a5648fa23b2f3767262ca408559400439af8c7ce956f7fd3c8d0e6a | 836 | 1-21 (complete) |
| Services/EveMapper/InstanceRegistrationHelper.cs | 5df5b18266850685a8c70b0aaeb538c6efdaf4620189bee5d360b411fc0f4fe7 | 4727 | 1-119 (complete) |
| Tests/Services/EveMapper/InstanceRegistrationHelperTests.cs | 0117530bf3475f3727dd6710ef8cf907bb6657ed6b7f38babe16c4ab814e0a4e | 16828 | 1-418 (complete) |
| Models/Db/WHMapAccess.cs | 8e078dbb675772c796c22226f36349e9814ad6ebda2164e7321e185184a840be | 1394 | 1-47 (complete) |

## 3. Findings

### 3.1 Authorization handler chain (inspected source)

`EveMapperRequirementHandlerBase<TRequirement>` (complete file, 65 lines) is the single shared handler base. The visible call sequence in `HandleRequirementAsync` is:

1. Read `ClaimTypes.NameIdentifier`; if empty or not parseable as `int`, return without succeeding — an authenticated identity is required before any access decision.
2. Optionally obtain `clientId` from `IBrowserClientIdProvider.GetClientIdAsync()`. The source comment states the `client_uid` cookie is client-supplied and must NOT be trusted on its own.
3. If a client id exists, call `_userManagementService.GetAccountsAsync(clientId)`. If the authenticated character id is in that account group, resolve the group's `primaryAccount` via `GetPrimaryAccountAsync(clientId)` and authorize **only** `primaryAccount.Id` through the abstract `IsAuthorizedAsync`, then return. If `primaryAccount` is null, the `if (primaryAccount != null)` block has no `return` in the null case, so execution falls through to the direct authenticated-character authorization check in step 4; fail-closed on that branch is not current source behavior.
4. Otherwise fall back to authorizing the authenticated character id directly via `IsAuthorizedAsync(authenticatedCharacterId)`.
5. `context.Succeed(requirement)` only when the chosen `IsAuthorizedAsync` returns true.

**Claim supported:** every authorization decision funnels through one abstract method; no handler performs its own claims parsing. **Limit:** `IsAuthorizedAsync` is abstract; the concrete handlers below delegate to `IEveMapperAccessHelper`, whose implementation is not supplied. Runtime behavior (fail-closed vs fail-open on helper exception, caching, revocation) is not evidenced. Invalidated by: any supplied `IEveMapperAccessHelper` implementation or handler registration that differs. Also, neither awaited `IsAuthorizedAsync` call is wrapped in `try/catch`, so a helper exception propagates out of the handler rather than being converted into an unsatisfied requirement (carried into section 6 item 9).

`EveMapperAccessHandler` (21 lines, complete): `IsAuthorizedAsync(int eveCharacterId) => _eveMapperAccessHelper.IsEveMapperUserAccessAuthorized(eveCharacterId)`.

`EveMapperAdminHandler` (21 lines, complete): same shape; delegates to `IsEveMapperAdminAccessAuthorized(eveCharacterId)`.

**Claim supported:** user access and admin access are separate policy requirements backed by separate helper methods. **Limit:** helper bodies, policy registration, and which endpoints require admin vs user policy are absent from the pack.

### 3.2 Per-map access entries and the empty-list policy (inspected source)

`WHMapAccess.cs` (47 lines, complete) models one grant row: `Id` (key), `WHMapId` (required), `EveEntityId` (required int; EVE character/corporation/alliance id), `EveEntityName` (required, StringLength 255), `EveEntity` (`WHAccessEntity` enum), `GrantedAt` (default `DateTime.UtcNow`), navigation `WHMap`.

The source comment states:

> "When no access entries exist for a map, all instance members can access it. When at least one access entry exists, only explicitly granted entities can access the map."

**Claim supported:** upstream implements a permissive empty-list default (all instance members) that flips to explicit-grant-only once any row exists. **Limit:** this is a data-model comment plus EF attributes; no query, repository, or middleware enforcing it is supplied. Whether "instance members" means all actors in the instance or only authenticated characters is unresolved. Invalidated by: an access-enforcement implementation reading `WHMapAccess` differently, or an owner decision changing the default (OD-13).

This conflicts with the MAP-042 candidate's proposed `explicit-grant-only` default (§5 R06 and §11 OD-13), which is labelled proposed pending owner decision. The upstream file is evidence of one existing design, not adopted policy.

### 3.3 First-owner bootstrap and instance registration (inspected source + tests)

`InstanceRegistrationHelper` (119 lines, complete) implements `IInstanceRegistrationHelper`.

`LoadRegistrationContextAsync(string? clientId)`:
- null/empty clientId → context with `IsAuthenticated = false`, `CharacterId = 0`.
- `GetPrimaryAccountAsync(clientId)` null → unauthenticated context.
- Otherwise sets `IsAuthenticated = true`, `CharacterId = primaryAccount.Id`.
- `GetCharacter(characterId)` failure → authenticated context without character info (empty name; corp/alliance lookups skipped). Success fills `CharacterInfo`, `CharacterName`, and looks up corporation/alliance names via `GetCorporation` / `GetAlliance` only when `CorporationId > 0` / `AllianceId > 0`.
- `GetAdministeredInstancesAsync(characterId)`: if any exist, sets `AlreadyHasInstance = true` and `ExistingInstanceId = first.Id`.

`RegisterInstanceAsync(context, instanceName, description, ownerType)`:
- `Character`: owner = `context.CharacterId`/`CharacterName`.
- `Corporation`: requires `CharacterInfo != null && CorporationId > 0`, else `InvalidOperationException("Corporation information not available")`; owner = character's corporation id/name.
- `Alliance`: requires `CharacterInfo != null && AllianceId > 0`, else `InvalidOperationException("Alliance information not available")`; owner = alliance id/name.
- Other enum values → `InvalidOperationException("Invalid owner type selected")`.
- `IsInstanceCreationLockedAsync()` true → `InvalidOperationException("Permission denied: instance creation is locked on this server")`.
- `!CanRegisterAsync(ownerEntityId)` → `InvalidOperationException("An instance already exists for this entity")`.
- Otherwise calls `CreateInstanceAsync(name, description, ownerEntityId, ownerEntityName, ownerType, context.CharacterId, context.CharacterName)` — the creating character id and name are recorded.

**Claim supported:** registration requires an already-authenticated primary account; owner may be a character, corporation, or alliance; instance creation can be globally locked and is limited to one instance per owner entity; the creating character is recorded. **Limit:** `CanRegisterAsync`, `CreateInstanceAsync`, `GetAdministeredInstancesAsync`, and the lock flag are service abstractions with no supplied implementation; no "first owner" seed or designation of an initial administrator when no instance exists yet is visible (OD-10). The tests mock every dependency, so no ESI call, database write, or HTTP request is evidenced.

### 3.4 Corporation/alliance/character membership (inspected source)

Membership enters through ESI-derived character data: `Character.CorporationId` and `Character.AllianceId` (integers; 0 means none) are read by `ICharacterServices.GetCharacter`, and corporation/alliance display names are optionally fetched from `IEveMapperService`. `WHMapAccess.EveEntity` (`WHAccessEntity` enum) and `EveEntityId` allow grants to characters, corporations, or alliances; `InstanceRegistrationHelper` registers an instance owned by any of the three.

**Claim supported:** character → corporation → alliance linkage is read from character data at registration/lookup time; no membership table, sync job, or roster-change propagation is supplied. **Limit:** membership staleness, leaves/kicks, and whether grant rows survive membership end are not addressed. Invalidated by: a membership-sync implementation or owner policy on lapsed membership.

### 3.5 Administrator boundaries (inspected source; partial)

`EveMapperAdminHandler` delegates admin checks to `IEveMapperAccessHelper.IsEveMapperAdminAccessAuthorized`. `InstanceRegistrationHelper` records `context.CharacterId`/`CharacterName` as creator on `CreateInstanceAsync`, but no supplied code defines what an instance administrator may do, whether the creator is auto-granted admin rights, or how map admin differs from instance admin. `WHMapAccess` rows carry `EveEntity` but no role enum is visible in the pack (MAP-042 proposes `viewer/editor/mapAdmin`, proposed only).

**Claim supported:** an admin authorization handler type exists; its decision logic and the admin↔creator relationship are missing from the pack. **Limit:** administrator boundaries cannot be evaluated from supplied files. Invalidated by: any supplied admin policy implementation.

### 3.6 Cache invalidation limitations (inspected source; gap)

The base handler's central trust claim is the `client_uid` boundary: the cookie is client-supplied and is honored only after the authenticated character is proven to belong to that client's account group; otherwise the handler falls back to the authenticated character directly. No server-side cache, token store, session, or invalidation event appears in any supplied file. `GrantedAt` defaults to `UtcNow` but no expiry, revocation, or cache-key invalidation on membership/grant change is visible.

**Claim supported:** client-supplied client ids cannot by themselves prove group membership; the handler mitigates this by requiring primary-account identity proof. **Limit:** cache invalidation on grant revocation, membership change, or logout is not evidenced anywhere in the pack; a revoked external token is not shown to clear local state (consistent with MAP-042 OD-07/OD-09). Invalidated by: a supplied cache/invalidation layer.

## 4. Call-relationship trace (visible in supplied files only)

| Caller | Target | Visibility |
|---|---|---|
| `EveMapperRequirementHandlerBase.HandleRequirementAsync` | `ClaimTypes.NameIdentifier` read; int parse | supplied |
| | `IBrowserClientIdProvider.GetClientIdAsync()` | interface, no implementation |
| | `IEveMapperUserManagementService.GetAccountsAsync(clientId)` | interface, no implementation |
| | `IEveMapperUserManagementService.GetPrimaryAccountAsync(clientId)` | interface, no implementation |
| | abstract `IsAuthorizedAsync(id)` | implemented by concrete handlers |
| `EveMapperAccessHandler.IsAuthorizedAsync` | `IEveMapperAccessHelper.IsEveMapperUserAccessAuthorized(id)` | helper, no implementation |
| `EveMapperAdminHandler.IsAuthorizedAsync` | `IEveMapperAccessHelper.IsEveMapperAdminAccessAuthorized(id)` | helper, no implementation |
| `InstanceRegistrationHelper.LoadRegistrationContextAsync` | `GetPrimaryAccountAsync`, `GetCharacter`, `GetCorporation`, `GetAlliance`, `GetAdministeredInstancesAsync` | all interfaces, no implementations |
| `InstanceRegistrationHelper.RegisterInstanceAsync` | `IsInstanceCreationLockedAsync`, `CanRegisterAsync`, `CreateInstanceAsync` | all interfaces, no implementations |
| `InstanceRegistrationHelperTests` | mocks all the above via Moq/AutoFixture | tests supplied, not executed here |

**Missing code vs proved behavior:** every service behind the handlers and registration helper is an interface with tests mocking it. Proved: the orchestration logic (guard clauses, owner-type switch, lock/can-register checks) as written. Not proved: any runtime enforcement, database persistence, ESI integration, or helper decision. No `try/catch` surrounds either awaited `IsAuthorizedAsync` call, so helper exceptions propagate and abort the request rather than producing a clean denial.

## 5. OD-09/10/13/14 mapping

| Decision | MAP-042 reference | Access-pack evidence | Status |
|---|---|---|---|
| OD-09: unseen handler implementations; per-handler authorization must be implemented and tested | §11, WH-F09 | `IEveMapperAccessHelper` bodies missing; access/admin handlers are thin delegates; no try/catch around awaited calls | Unresolved — no handler logic supplied |
| OD-10: bootstrap actor/initial owner designation | §7 WH-042-API-13..16; OD-10 | Registration requires an existing authenticated primary account; no first-instance seed visible | Unresolved |
| OD-13: explicit-grant-only vs permissive empty-list default | §5 R06; OD-13 | `WHMapAccess`: empty list ⇒ all instance members; rows ⇒ explicit grants only (upstream permissive default) | Unresolved — owner decision; upstream behavior documented but not adopted |
| OD-14: opt-in default, sharing expiry, per-jump vs continuous | §5 R07; OD-14 | No consent, location-sharing, or expiry code in the access pack | Unresolved — no evidence supplied |

## 6. Negative-case test proposals (not executed; source-linked)

None of these were executed; none constitute security evidence. Each proposal references specific fields, messages, or control paths from the inspected source only.

1. Base handler, non-integer `NameIdentifier`: `TryParse` fails → handler returns without `Succeed`. Expected: no authorization, no exception. Not covered by supplied tests.
2. Base handler, client id present but authenticated character not in the account group: skip primary path; fall back to direct `IsAuthorizedAsync(authenticatedCharacterId)`. Expected: direct check applies; no inheritance of primary rights. Not covered.
3. Base handler, primary account null after group match: execution falls through to `IsAuthorizedAsync(authenticatedCharacterId)` per `EveMapperRequirementHandlerBase.cs`. Expected: direct-character fallback; not fail-closed on that branch. Unexecuted, source-linked only.
4. Registration, invalid `WHAccessEntity` cast `(WHAccessEntity)999`: `InvalidOperationException("Invalid owner type selected")`. Covered by fixture `RegisterInstance_WhenInvalidOwnerType_ThrowsInvalidOperationException`.
5. Corporation owner with missing `CharacterInfo`: `InvalidOperationException("Corporation information not available")`. Covered by fixture.
6. Alliance owner with `AllianceId = 0`: `InvalidOperationException("Alliance information not available")`. Covered by fixture.
7. Creation locked / `CanRegisterAsync` false / duplicate entity: covered by fixtures; expected messages as in §3.3.
8. Helper `IsEveMapperUserAccessAuthorized` / `IsEveMapperAdminAccessAuthorized` returns `false`: `context.Succeed` is not called, so the requirement is left unsatisfied; expected clean denial, no exception. Not covered by supplied tests.
9. Helper throws: `HandleRequirementAsync` awaits `IsAuthorizedAsync` with no `try/catch` on either the primary-account path or the direct fallback, so the exception propagates out of the handler and aborts the request; it is not converted to an unsatisfied requirement. Cannot be concretized until `IEveMapperAccessHelper` implementations exist (OD-09).
10. Empty-list enforcement: map with zero `WHMapAccess` rows accessed by a non-member instance actor → expected behavior depends on OD-13; under the upstream model access is granted, under MAP-042's proposed default denied. No single expected result can be fixed until OD-13 is decided.

## 7. Candidate amendments (proposed, not mandates; owner choices preserved)

1. Record the `client_uid` trust boundary as a documented security assumption requiring verification: client-supplied cookie never trusted alone; primary-account identity proof required first (from `EveMapperRequirementHandlerBase`). Treat as assumption, not implemented control.
2. Supply `IEveMapperAccessHelper` implementations before any authorization acceptance (OD-09); without them, user/admin handler behavior is unknown.
3. Define the first-owner/bootstrap seed (OD-10): how the first instance and its administrator are created when no authenticated primary account or instance exists yet. `InstanceRegistrationHelper` presupposes both.
4. Decide empty-list vs explicit-grant-only default (OD-13): upstream `WHMapAccess` is permissive-by-default; MAP-042 proposes explicit-grant-only. Either is an owner choice; the chosen rule must be enforced by code not yet supplied.
5. Add a consent/expiry model for location sharing (OD-14): no consent code appears in the access pack; opt-in default, sharing expiry, and per-jump vs continuous remain open.
6. Define cache invalidation on grant revocation, membership change, and logout (OD-07/OD-09): absent from all supplied files; a revoked external token is not shown to invalidate local state.

## 8. Comparison with MAP-042 blueprint (proposed alternatives, not accepted policy)

The MAP-042 candidate (unaccepted) proposes an explicit-grant-only default, `viewer/editor/mapAdmin` roles, UUID actor/map/grant entities, server-derived identity, and bootstrap ops API-13..16 out of MVP with the bootstrap actor unresolved. The access pack shows an int-based EVE entity model (`EveEntityId`, `WHMapId` int), a permissive empty-list default, no role column, and registration predicated on an existing authenticated character. These are alternative upstream designs for reference only; no stack, identifier scheme, or default is selected by this report. Alignment between MAP-042's proposed schema and upstream behavior is a future owner decision.

## 9. Limitations and missing evidence

- No `IEveMapperAccessHelper`, `IEveMapperUserManagementService`, `IEveMapperInstanceService`, `ICharacterServices`, or `IEveMapperService` implementation is supplied; all runtime authorization is unverified.
- The tests in `InstanceRegistrationHelperTests.cs` were read, not executed; Moq/AutoFixture fixtures prove test design, not server behavior.
- No ESI OAuth, scope, rate-limit, or issuer metadata is in this pack (covered by separate research packets).
- No root licence conflict exists between inspected MIT roots (Pathfinder and EVE-WHMapper); transitive licences, assets, game data, and the CCP agreement remain unchecked (MAP-042 §4).
- No first-owner seed, cache invalidation layer, or membership-sync code is present; cache invalidation on revocation/membership change is an explicit gap.
- The null-primaryAccount fall-through behavior in §3.1 step 3 is a source-reading detail, not a security conclusion; it does not by itself establish fail-open or fail-closed runtime behavior.

## 10. Remaining work and review pending

Owner decisions required: OD-09 (handler implementation evidence), OD-10 (bootstrap actor), OD-13 (access default), OD-14 (consent/expiry). Missing source evidence: `IEveMapperAccessHelper` implementations, handler registration, any enforceable access query over `WHMapAccess`, and a cache invalidation mechanism. This report is a research input only: it does not accept, amend, or override the MAP-042 blueprint; it proposes amendments for owner review. Review pending: coordinator review of this report, then consolidation into the evidence register with proposed amendments.
