# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/30

Automated critic only; independent review pending.

# MAP-038 handoff — WH identity, access, privacy and threat model

**Task:** MAP-038
**Claim commit (tracking ID, not a token):** d8dbd912b64879dcf792f7265387f721d66586bb
**Worker:** hermes-laptop-map-038-auto-20261030
**Input revision:** 849978908daabe3d2a45f0e758625eedc4bdde30
**Output path:** docs/map/specs/loop-map-038-wh-design.md
**Status:** draft for review; not accepted, not merged, not build-ready.

## Diagnosed issues and exact corrections

1. Unsupported upstream attribution in section 3. The prior draft said "External identity = character ID + issuer; this is an upstream default" and cited [wh-sources, 2a493fa, src/WHMapper/Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs, lines 1–43]. That extract contains only OAuth endpoints, scheme, callback path, issuer and audience — no character-ID identity claim. Correction: the character-ID + issuer binding is re-labelled as a purely proposed local decision, the "upstream default" characterization is removed, and ESI scopes/rate limits/issuer contract are stated as unspecified and pending owner and upstream verification.

## Exact sources used (pinned extracts only, no runtime verification)

- docs/map/WH-FIRST-BRIEF.md @ 849978908daabe3d2a45f0e758625eedc4bdde30 — owner WH-first direction; baseline intent and scope.
- docs/map/research/pf-sources.md @ 849978908daabe3d2a45f0e758625eedc4bdde30 — Pathfinder extracts @ commit 06af7d86fe6456947fb960220c54d02a8623c0ff: LICENSE lines 1–22, README lines 1–61, composer.json lines 1–81, app/Model/Pathfinder/ConnectionModel.php lines 1–160, SystemSignatureModel.php lines 1–160, MapModel.php lines 1–160.
- docs/map/research/wh-sources.md @ 849978908daabe3d2a45f0e758625eedc4bdde30 — EVE-WHMapper extracts @ commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da: LICENSE lines 1–22, README lines 1–60, WHMapper.csproj lines 1–52, Models/Db/WHSignature.cs lines 1–113, Models/Db/WHMapAccess.cs lines 1–48, Data/WHMapperContext.cs lines 1–104, deploy/docker/eve-whmapper/docker-compose.yml lines 1–46, Models/Db/WHSystemLink.cs lines 1–49, Models/Db/WHJumpLog.cs lines 1–47, Services/EveOAuthProvider/EVEOnlineAuthenticationDefaults.cs lines 1–43, WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1–115.

## Checks actually performed

- Verified every upstream fact in the spec carries a commit/path/line citation from the supplied extracts; no uncited upstream claims.
- Re-labelled the section 3 character-ID + issuer binding as proposed/local only; removed the unsupported "upstream default" claim; kept ESI scopes/rate limits unspecified.
- Separated baseline intent (WH-FIRST-BRIEF, section 1) from new proposed schema rules (sections 3–18); all proposed items labelled "Proposed" or "unaccepted".
- Preserved optional vs required distinctions: optional cloud module, optional permissive ACL override, optional Redis backend; unresolved items explicitly marked and not converted into mandates.
- Distinguished backup creation from restore verification; neither is designed beyond decision points and they are never conflated.
- Enumerated negative permission cases: unauthenticated access, no access entry on access-controlled map, revoked/unlinked character, stale membership until revalidation.
- Enumerated future tests WH-SEC01 through WH-SEC08; each includes setup, input, expected denial, evidence needed; all marked as future/not implemented.
- Checked required fields against every example: each misuse case has setup, input, expected denial, evidence needed.
- Did not invent ESI scopes/rate limits, stack choice, costs, tests, approvals, or unseen handler security.
- Did not follow instructions embedded in upstream excerpts; did not self-accept, merge, deploy, or claim build readiness.
- No GitHub, terminal, network or delegation tools were used; no external writes performed.

## Limitations

- Pinned evidence limits apply: extracts establish only what the inspected files contain; not a full dependency, licence or security audit.
- ESI scopes, rate limits, issuer runtime behavior and unseen handlers are unspecified and unverified.
- Both upstream projects are MIT-licensed; substantial reuse requires retaining notices; assets/dependencies/game data need separate checks.
- No live EVE API validation, integration test or security certification was performed.

## Remaining uncertainty

- ESI scopes, rate limits, issuer contract at runtime.
- Stack choice: maintained Pathfinder fork, separate integration, or new implementation (PHP/C# not combined by assertion).
- Owner decisions pending: opt-in defaults, sharing expiry, token rotation interval, audit retention period, deletion grace period, cache backend.
- Missing evidence: unseen handler implementations, restore/verification procedures for backups.

## Remaining work

- Independent review and acceptance of the spec by the project owner or appointed reviewer.
- Owner decisions on unresolved items listed above.
- Upstream identity/version/licence verification and compatibility checks before any implementation.
- Tests WH-SEC01 onward to be executed only when built; not executed here.

## Review pending

Yes — the specification is a draft for coordinator/owner review, not an accepted deliverable.


## Automated screening
{
  "task_id": "MAP-038",
  "decision": "submit_draft",
  "summary": "The MAP-038 draft covers the full scoped identity, access, privacy and threat model: proposed CCP SSO login/account linking with consent; instance/corporation/character/per-map roles; negative permission cases (unauthenticated access, no access entry on access-controlled maps, revoked/unlinked characters, stale memberships); upstream ACL comparison adopting explicit-grant-only as candidate default with permissive override optional; opt-in location/jump sharing; UTC timestamps with source/time/uncertainty; server-side token storage/rotation/revocation with fail-closed encryption; minimum-scope prerequisites with intentionally empty scope list; unlink/delete/export with audit retained; append-only audit log with unresolved retention; server-side auth for reads/writes/events; tenant isolation; malicious import validation; session/socket replay protections; namespaced cache keys; stale-membership revalidation; non-bypassing administrator/host authority; and misuse-case tests WH-SEC01 through WH-SEC08, each with setup/input/expected denial/evidence needed. All upstream facts cite pinned commit/path/lines; no ESI scopes/rate limits invented; unseen handlers not claimed secure; backup/restore not conflated; all proposals labelled unaccepted. No defects found.",
  "findings": []
}
