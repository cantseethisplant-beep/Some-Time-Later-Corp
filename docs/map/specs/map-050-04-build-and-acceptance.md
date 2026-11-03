# Two-module build sequence and acceptance map

Planning only. No steps below have been executed by the app. “Pass” must refer to an actual stored result, not this document. Preserve source pins and reuse valid evidence until its stated invalidation condition changes; do not repeat unrelated broad audits.

## 1. Versioned build inputs

Record base commit `2a493fad9acec9a8e15b619f7943ae8b6e7f30da`, integration patch hash, Tools/Hosting versions, module schema versions, resolved dependency locks, image digests/architectures, .NET SDK and deployment profile. Keep provider secrets outside Git. A compatibility manifest must make mismatches visible and prevent loading an incompatible module.

Base integer IDs and module UUIDs are distinct types. The older all-UUID candidate is historical and does not authorize a migration of WHMapper PKs. Root MIT source does not settle transitive dependency/asset/game-data terms; distribution and monetization remain gated by actual review.

## 2. Implementation order

| Step | Prerequisites | Deliverable | Observable acceptance |
|---|---|---|---|
| M-B00 Baseline freeze | Owner review of this proposed module direction; source/terms inventory | Exact source/dependency/image records, compatibility manifest, private build layout and synthetic fixture profile | M-T01: all inputs reproducible and unresolved licence/version decisions explicit; no mutable release identity |
| M-B01 Untouched mapper baseline | B00 | Selected base compiles/runs in an isolated test environment; known core routes/workflows recorded | M-T02: login/map/paste/route/event smoke checks recorded; no claim README features work until observed |
| M-B02 No-op integration bridge | B01 | Explicit startup/service/UI/event adapters, both modules off, module migrations isolated | M-T03/M-T04: baseline still works with modules disabled; incompatible version and orphan map fail closed; no new public anonymous endpoint |
| M-B03 Tools vertical slice | B02, explicit owner/grants and consent model | One source-stamped system annotation end to end | M-T05/M-T06: authorized create/read/update; typed IDs and same-map relations; other map/actor denied; secret-free UI/errors |
| M-B04 Tools conflict/staleness/sharing | B03 | Revision conflict UI, scan preview, age/uncertainty overlay, consent-revocation flow and scoped export | M-T07/M-T08/M-T09: no lost updates, no destructive scan omission, stale/unknown data labelled, no revoked event/cache/replay leakage |
| M-B05 Oracle/Cloudflare qualification | B02; ARM/image viability, actual free quota/region and approved domain/backup custody | Bounded pilot profile with tunnel, HTTPS/SSO/WebSockets, private data services, restore and measured resource evidence | M-T10/M-T11/M-T12: direct-origin bypass denied, callback/sessions work, reconnection and isolated restore proven; measured load fits selected limit |
| M-B06 Hosting read-only slice | B02; separate hosting role and offer consent | Health/offer inventory, request/approval ledger; provider execution disabled | M-T13/M-T14: no remote effect from record creation; tenant/host-owner scope, expiry/idempotency and controller-outage states correct |
| M-B07 Optional provider execution | B06; separately approved operation schemas/keys/quotas and rollback | One allowlisted non-destructive adapter operation, then separately reviewed lifecycle expansion | M-T15: exact approved effect, no arbitrary command/URL, uncertain timeout reconciled without duplicate effect, revoke/expiry stops execution |
| M-B08 Release/upgrade handoff | Selected slices qualified; terms/security/recovery gates met | Frozen release record, support/runbook, rollback/forward recovery and owner acceptance | M-T16: upgrade preserves IDs/grants/data, disable preserves core, rollback/restore evidence and release scope truthful |

B03 and B06 are independent after B02. B05 can qualify the base/bridge before Tools/Hosting features are live. B07 is optional and must not hold the basic mapper/Tools release hostage. No deployment or app implementation is started merely because these steps are written.

## 3. Focused checks

| Check | Setup/input | Expected observable result / required evidence |
|---|---|---|
| M-T01 Source identity | Fresh checkout/build inputs at recorded versions | source/patch/lock/image hashes match; unpinned dependency resolution is recorded and frozen before release |
| M-T02 Base smoke | Isolated fixture tenant and authorized test actor | actual mapper read/edit/paste/route/event outcomes recorded; failures classified without deleting evidence |
| M-T03 Modules disabled | Base+bridge, both module flags off | qualified base functions remain; no module routes/events/controller calls or destructive migration |
| M-T04 Adapter/type gates | Map with null WHInstanceId; wrong-map system; incompatible base/module version | module rejects unresolved identity/type/version before data disclosure; base PKs unchanged |
| M-T05 Tools happy path | Map 42/system 301 and explicit module grant | one annotation UUID, revision/event and source/time retained after restart; actor derived from session |
| M-T06 Access/markup | Different tenant, read-only actor, hostile note markup and export attempt | denied read/write/export/event and safe rendering; no current private body or token in error/cache |
| M-T07 Concurrent scans | Two clients edit same revision; repeated idempotency key; changed payload | exactly one ordinary update, visible conflict; same key/same intent no duplicate; changed intent rejected |
| M-T08 Observation boundaries | Unknown mass, old/manual intel, repeated signature, location polling gap | uncertainty/age visible, missing pasted row not auto-deleted, no exact-mass/hostile/safe-route assertion |
| M-T09 Revocation/offline | Sharing on, subscribed client/cache, then revoke and replay queued write; remote revoke fails | local module delivery/cache/session policy closes immediately; replay denied; remote failure shown separately; base tracking behavior explicitly tested |
| M-T10 Edge/proxy | Named Cloudflare route plus direct-origin attempt and forged forward headers | public HTTPS/SSO return URL correct; private routes not cached; direct app/database access denied; only configured proxy trusted |
| M-T11 Real-time/outage | Blazor/hub connection, tunnel restart and backend restart | expected disconnect/reconnect with reauthorization; no cross-map subscription restoration; no claim WAF inspects post-handshake frames |
| M-T12 Capacity/restore | Proposed small pilot load and isolated restore with base+module data | measured CPU/RAM/DB/latency within chosen envelope; compare IDs, revisions, grants, timestamps and events after restore; key custody and revocation documented |
| M-T13 Offer/approval | Owner offer, other-tenant request, expired or modified approval | pending record has no provider effect; wrong owner/tenant/expiry or payload hash rejected |
| M-T14 Controller outage | Controller unreachable; external-managed active backend | health unknown/controller-unavailable; no hidden execution; active backend cannot be terminated from its own module |
| M-T15 Adapter effect | One approved allowlisted operation, duplicate delivery, timeout and revocation | correlation/effect reconciled once; no scope expansion, paid upgrade or arbitrary shell; redacted receipt and rollback path |
| M-T16 Upgrade/disable | Recorded compatible base/module pair, backup and older release | migrations preserve identity/ownership; rollback or forward recovery proven; uninstall does not delete core maps/live workloads |

The initial capacity profile is a **proposed qualification target**, not measured capacity: five simultaneous fixture clients performing normal map reads and 100 combined module edits over five minutes, no unhandled errors, and an operator-approved latency/resource ceiling recorded before running the check. Increase target population only after measurement. Never burn artificial CPU/network load to evade an idle-instance policy.

## 4. Requirement traceability

| Requirement | Build steps | Checks |
|---|---|---|
| MOD-R01 Reuse mapper, preserve base data/identity | M-B00..02 | M-T01..04 |
| MOD-R02 Independently versioned, optional modules | M-B02, M-B08 | M-T03, M-T04, M-T16 |
| MOD-R03 Evidence-stamped Tools workflow | M-B03..04 | M-T05, M-T08 |
| MOD-R04 Tenant/module authorization and explicit consent | M-B02..04 | M-T04, M-T06, M-T09 |
| MOD-R05 Conflicts, uncertainty and honest offline state | M-B04 | M-T07..09 |
| MOD-R06 Hosting offer/request/approval separation | M-B06 | M-T13..14 |
| MOD-R07 Bounded provider authority, no hidden cost/remote action | M-B07 | M-T14..15 |
| MOD-R08 Cloudflare midpoint / Oracle backend option | M-B05 | M-T10..12 |
| MOD-R09 Recovery, upgrades and source/licence traceability | M-B00, M-B05, M-B08 | M-T01, M-T12, M-T16 |

Ranges above refer only to the defined step/check IDs. Every release must state which optional slices it includes; a read-only Hosting release cannot advertise automated deployment.

## 5. Remaining gates, not repeated research loops

Before implementation: review this proposed compile-time module/bridge contract and the owner bootstrap/default policies. Before copying/distribution: inspect actual resolved licences/assets/CCP terms and record notices. Before Oracle: confirm account/home-region capacity, actual Always Free eligibility and all dependent service costs; verify ARM64 images/builds and backup custody. Before live users: qualify authorization, consent/revocation, WebSocket/proxy and restore behavior. Before any provider operation: explicit credentials/scopes/approval/idempotency and no paid fallback.

Those are concrete implementation/release artifacts. Existing source facts and hash-bound research are reusable within their versions; runtime acceptance cannot be fabricated by re-auditing prose.
