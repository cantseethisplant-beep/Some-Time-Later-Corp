# Ordered build contract and release evidence

No implementation steps or app tests in this document have run. Evidence state for every Q check below starts `NOT_RUN`. A passing document/schema fixture is not a Q runtime pass. The specification is deliberately finite; fix an actual failing contract, do not repeat a general audit.

## Build graph and deliverables

| Step | Needs | Concrete deliverable / stop condition |
|---|---|---|
| P0-B00 Freeze inputs | Independent design review | Private source copy at pinned base; source/patch/module/schema identities; SDK/package lock and transitive inventory; resolved image architecture digests, licences/assets/notices; synthetic fixture configuration. Stop if required terms/dependency identity unresolved |
| P0-B01 Untouched base | B00 | Isolated compile/run of unchanged base; record existing login/map/system/paste/route/hub workflow. No live player credentials: mock SSO/ESI fixture identities. Stop if baseline fails; do not blame modules |
| P0-B02 Bridge and startup safety | B01 | Compile-time registrations, actor/map adapter, invalidation/gates, protected key directory, migration/readiness patch; both modules off. Required patch inventory in 08; stop if seams cannot be covered |
| P0-B03 Tools data/API | B02 | Schema/handlers from 02/03/09; pairing/grants/consent; idempotent module-only note writes; no core signature mutation |
| P0-B04 UI/events | B03 | Source/time/stale labels, conflict display, delete, no-persistence drafts, per-recipient invalidation/reauthorization and correct disabled states |
| P0-B05 Operating qualification | B04 | Migration failure evidence; encrypted off-host backups/journal receipt; isolated restore; latency/resource run and recovery runbook |
| P0-B06 Optional Hosting ledger | B02 | Exactly 07 read-only offers/request/approval UI/API; no adapters/SDK/agent commands. Independent of Tools B03..05 |
| P0-B07 Optional cloud pilot | B05 plus actual deployment profile | Oracle eligibility/capacity/ARM images/domain, Cloudflare named tunnel/proxy/cache/SSO/hub/recovery evidence; no existing physical server or automatic paid fallback |
| P0-B08 Freeze release | Selected preceding steps qualified | Immutable release manifest, redacted evidence index, included/deferred features, operator runbook, independent approval. Product claim limited to observed selected scope |

Private future layout: `upstream/WHMapper`, `modules/WhTools`, `modules/Hosting`, `integration/WhMapperBridge`, `tests`, `deploy`, `operations`. Integration patch manifest lists every changed upstream path with base/patch hash and reason. No runtime arbitrary module loader. P0 Tools version 0.1.0, Hosting ledger 0.1.0, bridge contract 1 and Tools schema/API 1; these are selected planned versions, not published binaries. A compatible manifest pins all four and base commit; mismatch disables the affected module, not a hidden upgrade.

## Required future qualification checks

| Check | Exact fixture/action | Required observable result |
|---|---|---|
| Q01 | Fresh locked build on selected platform | Recorded base/SDK/locks/image digests; dependency/asset notices accounted; compile result and logs privately retained |
| Q02 | Untouched baseline synthetic users, maps 42/43, systems 301/302 | Base login/map/edit/paste/route/hub observed; tests use verified fixture identity, no production tokens |
| Q03 | Both modules off; incompatible Tools version/schema | Base qualified functions survive; no Tools/Hosting routes/events/jobs; mismatch not silently loaded |
| Q04 | Unknown/orphan map, wrong-map system, string/int confusion | Generic denial/invalid payload; no foreign current record, no invented instance |
| Q05 | First-owner pairing twice; transfer; lost owner recovery | No anonymous self-claim; one owner; stale/absent admin denied; recovery revokes instance grants/consents |
| Q06 | View-only member, non-sharing viewer, sharing annotator, other character | Matrix in 01 enforced; non-sharing read permitted, create/edit denied; alts do not union privileges |
| Q07 | Forge actor/source/corroborated/system/map fields | Unknown/immutable fields rejected; only manual/reported created; verified actual author recorded |
| Q08 | Invalid text/Unicode/body size/time/revision/unknown JSON keys | Exact schema/semantic errors, no effect; hostile HTML rendered literally |
| Q09 | Two edits at revision 1; same key same/different payload; lost response | One revision increment; authorized 409; identical retry original result; changed payload conflict; no duplicate after uncertain commit |
| Q10 | Consent expires/disables, grant revoke, character switch/unlink, failed remote revoke | Correct distinct actions; local shutdown independent of remote error; queued write denied; old success cannot disclose data |
| Q11 | Corp change with cached membership, stale/unavailable membership, local base ACL change | Evidence age <=300 seconds; expiry/outage denies; no duplicate early ESI polling; local invalidation enforced before acknowledgment |
| Q12 | Cross-origin/missing CSRF, forged forward headers, callback | Module mutations denied as specified; trusted proxy only, SSO survives; no private HTTP caching |
| Q13 | Unauthorized hub subscribe, connection resume, dropped/duplicate/out-of-order events | No private content in invalidations; per-recipient authorization; refetch after resume/gap; no restored cross-map subscription |
| Q14 | Offline edit then revoke then retry; tab close/character switch | Unsaved memory draft clearly labelled; no browser persistence/hidden queue; retry reauthorized; cleared on switch/close |
| Q15 | Concurrent delete/expiry/core map deletion/reparenting | Text removed/tombstone revision; no cascade core deletion; active module references block base destructive change; no resurrection through retry |
| Q16 | Inject transaction/outbox send/DB serialization failure | No precommit success/half write; bounded identical-intent retries; committed note remains after event-send failure; refetch correct |
| Q17 | Missing key directory/cert, incompatible/pending migration, two deployment jobs, mid-migration failure | Shared/base failure: no product ingress and nonzero bounded startup; module-only mismatch: affected routes absent, qualified base may serve but required-module release not ready; one migration owner; failed deployment stays maintenance |
| Q18 | Export/import old Redis ring, rotate cert, restart with retained protected fixture values | Actual continuity where required; ring/cert custody correct; unknown durable Redis state blocks approval |
| Q19 | Daily backup unavailable/too old; journal receiver offline/unknown receipt | Writes degrade as specified; security operation suspended, not falsely acknowledged; same-intent reconciliation safe; no paid fallback |
| Q20 | Restore older generation after note deletion and access revoke | Journal replay and all-session/grant invalidation prevent resurrection; integer/UUID identities consistent; fresh login only; measured RPO/RTO targets met |
| Q21 | Retention fixture clock advances 30/90 days and backup seven days | Historical text, expired notes, metadata/backups purged at policy; reads filter immediately even before sweep; no live text in audit |
| Q22 | Five simultaneous fixture clients, 100 total edits over five minutes | No unhandled/5xx errors; p95 acknowledged local API latency <=2 seconds excluding external SSO/ESI; process+DB+Redis peak RAM <=75% selected VM RAM, average CPU <=80%, free disk >=20%; record environment and sample method |
| Q23 | Owner/other-tenant offers, same-actor approval, expired/changed request, controller missing | Optional Hosting follows 07; no provider effect, no imaginary healthy telemetry, no self approval or cross-tenant details |
| Q24 | Architecture-specific Oracle deployment with named tunnel; backend/tunnel restart; direct-origin probe | HTTPS/callback/SignalR reconnect reauthorizes; app/DB private; ARM images really run; current free quota/cost constraints verified |
| Q25 | Upgrade/disable/restore previous compatible release | Core IDs and ownership unchanged; module archive retained; rollback or reviewed forward recovery evidence; no remote/core deletion on disable |

Latency/load and recovery numbers are selected acceptance targets, not measured claims or EVE gameplay constants. Load exists only for bounded qualification, never to defeat free-instance idle policy. Failure means reduce advertised scope or review an explicit change; do not secretly loosen a passing threshold after observing results.

## Requirement/review traceability and selected release sets

| Review finding | Normative resolution | Runtime evidence |
|---|---|---|
| R01 | 01 consent/access/owner matrix | Q04..06, Q10..11 |
| R02 | 02 server-fixed manual provenance; later provenance disabled | Q07..08 |
| R03 | 03 module-only transactions; 04 no combined scan writes | Q09, Q15..16 |
| R04 | 05 explicit key migration/custody/recovery | Q18..20 |
| R05 | 05 single migration job and fail-closed readiness | Q17 |
| R06 | 01..03 and 09 exact schema/limits/session/events | Q06..16, Q21 |
| R07 | 00 scope; this graph/targets and release sets | Q01..25 as selected below |

P0 local Tools release requires Q01..22 and Q25; Q23 is mandatory only if Hosting ledger enabled; Q24 only for the cloud pilot. Q18 migration subcase applies to existing-key installs; a fresh install must still demonstrate key backup/rotation/recovery. Q02 base scenarios must be concretely enumerated in the evidence index, not reduced to a homepage screenshot. Deferred scan/route/export/provider capabilities cannot be advertised as qualified because notes work.

Each evidence record has check/subcase ID, state NOT_RUN/PASS/FAIL/BLOCKED/NOT_APPLICABLE, reason for N/A, input manifest hash, source/patch/module/environment identities, synthetic fixture revision, observed result, redacted artifact hash/path, UTC, reviewer, invalidation triggers and affected releases. No absent result defaults to PASS. Commit the private evidence index with public safe summary only. Independent acceptance remains a separate state.

## Stop conditions and remaining concrete inputs

Before component work, require actual .NET SDK, selected architecture build tools and isolated PostgreSQL/Redis/test identity environment. Inspection in this workspace on 3 November found dotnet launcher but no SDK listed, and no Docker command; a baseline compile/run cannot be honestly reported from that environment. This is a tooling prerequisite, not an unknown behavior in the specification. Installing tools/starting the actual implementation is a separate authorised work step.

Before cloud release, privately supply actual domain/SSO registration, account/home region/free quota, image architecture, secrets/certificate custody, off-host laptop backup+journal receiver configuration, administrator/recovery identities and support contact. The owner must acknowledge the declared retention/contribution/availability policy before live data. These are configuration/operating approvals, not things to fabricate in public docs. Oracle conditions are revalidated only when that option is used; quota/capacity failure blocks provisioning, never selects a paid fallback. Full repository build-ready acceptance waits for the required independent and component evidence; this text cannot waive that rule.
