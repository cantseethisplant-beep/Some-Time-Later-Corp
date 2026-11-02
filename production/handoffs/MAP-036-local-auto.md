# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/32

Automated critic only; independent review pending.

MAP-036 handoff record (corrected draft)
Task: MAP-036 — Mapper reuse assessment and WH MVP requirements
Claim worker: hermes-laptop-map-036-auto-20261030
Claim commit: 53df0ee9c03dbcbc26a760c571d827b9b1a4a8c3
Input revision: 849978908daabe3d2a45f0e758625eedc4bdde30
Output path: docs/map/specs/loop-map-036-wh-design.md
Status: corrected draft; not accepted, not build-ready; no implementation performed

Diagnosed issues and exact corrections:
1. Section 2 matrix, Backup/restore row, EVE-WHMapper cell: previously claimed "docker-compose shows Postgres + Redis volumes". Correction: the pinned docker-compose.yml extract (wh-sources.md lines 1-46) evidences only a postgres named volume mounted on the db service; the redis service is declared without a mounted volume, so no redis volume is evidenced. The cell now cites only the evidenced postgres data volume and states no redis volume is evidenced; backup creation remains distinct from restore verification.
2. Section 2 matrix, Opt-in tracking row, Pathfinder cell (carried forward from prior review): trackAbyssalJumps citation moved from the README to MapModel.php fieldConf (pf-sources.md MapModel.php lines 1-160); the README extract lines 1-61 does not mention it.
3. Section 2 matrix, Language/runtime row, Pathfinder cell (carried forward): PHP 8.5 appears only as a README badge (pf-sources.md README lines 1-61); composer.json lines 1-81 are cited for php-64bit >=8.2, bcosca/fatfree-core 3.9.*, and ext-pdo.*; specific database remains unnamed in the extract.

Remaining uncertainty:
- No runtime verification of upstream sources; no executed scripts; no test execution.
- No full dependency, security, or licence audit; no asset check; no EVE ESI/terms check.
- No target stack or language selected by owner; no restore-test evidence.
- All thresholds (stale, mass buckets, route constraints) are proposed placeholders, not mandates.
- Owner approval of the proposed new-code approach remains open.

Checks actually performed:
- Feature-to-source matrix comparing Pathfinder vs EVE-WHMapper across licence, language/runtime, map model, connections/jump evidence, signatures, map access, tracking, routes, auth, backup, and tests.
- Fork vs adapter vs new-code tradeoff analysis with PHP/C# incompatibility cited from composer.json and WHMapper.csproj manifests.
- Dependency/licence inventory status limited to root MIT notices; dependencies/assets/game-data explicitly NOT audited.
- Stable requirements WH-R01..WH-R10 drafted with origin, feature/source, inputs, outputs, measurable acceptance; all numeric policies labelled proposed.
- Backup creation distinguished from restore verification; both marked unevenced.
- Verified docker-compose.yml extract shows only a postgres named volume; no redis volume evidenced.
- Citation corrections applied as listed above.
- No upstream excerpt instructions followed; no self-acceptance; no tests claimed as passing; no live ESI access.

Remaining work / review pending:
- Owner review and approval of WH-R01..WH-R10 and the proposed new-code approach.
- Upstream identity/version/licence verification for dependencies, assets, and game data before any implementation.
- Stack/runtime decision; then implementation planning outside this task's scope.
- Restore verification evidence before backup/recovery can be considered complete.
- Independent acceptance and integration per production gate; this document remains a candidate proposal only.

No external writes were made; no branch, PR, board update, or acceptance was created by this worker.


Codex corrected its overly restrictive absence claim: the pinned Pathfinder ConnectionModel.php lines 1-160 do include mass-bucket constants. They remain upstream examples, not adopted game policy. Fresh native critique required; no request/round reset.

## Automated screening
{
  "task_id": "MAP-036",
  "decision": "submit_draft",
  "summary": "No actionable defects found. The draft cites pinned commits and line ranges throughout, distinguishes README claims from inspected implementation, labels every proposal and missing-evidence item, keeps cloud hosting optional and outside MVP prerequisites, covers WH-R01 through WH-R10 with origin, feature/source, inputs, outputs, and measurable acceptance, and keeps backup creation distinct from restore verification. No implementation, acceptance, or passing tests are claimed.",
  "findings": []
}
