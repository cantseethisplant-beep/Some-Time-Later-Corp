# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/31

Automated critic only; independent review pending.

MAP-039 | claim commit 434bf06096b019de9e5ac21ad2a54f990cba6842 | input revision 849978908daabe3d2a45f0e758625eedc4bdde30 | worker hermes-laptop-map-039-auto-20261030 | token AUovQx_xjciXAj2lBFsmCOBk8aTJpwQI | output docs/map/specs/loop-map-039-wh-design.md

Exact sources read: docs/map/WH-FIRST-BRIEF.md; docs/map/research/pf-sources.md (commit 06af7d86fe6456947fb960220c54d02a8623c0ff); docs/map/research/wh-sources.md (commit 2a493fad9acec9a8e15b619f7943ae8b6e7f30da). All commit/path/line citations point at those pinned extracts.

Diagnosed issue and exact correction:
- WH-T01 in the prior draft misstated the pinned EVE-WHMapper import tests. It had said "one unresolved + one wormhole signature → exactly one created, zero fully-scanned created", conflating two different cases and contradicting itself. Corrected WH-T01 now states (a) both signatures already present → Persisted true, FullyScannedCreatedCount 0, FullyScannedChangedCount 0; (b) empty repository → Create called with exactly 2 signatures, FullyScannedCreatedCount 1 (only the 100% row), FullyScannedChangedCount 0; and retains the partial 42.5% strength negative case (group resolved, FullyScannedChangedCount 0). Source: wh-sources, src/WHMapper.Tests/WHHelper/WHSignatureHelperImportTests.cs lines 1-115.

Checks actually performed: close reading of the three pinned inputs; cross-referencing upstream README claims against inspected model/source lines; distinguishing baseline intent from proposed design rules; verifying both root MIT licences are reproduced in the extracts; enumerating WH-B01..WH-B07 and WH-T01..WH-T11 with fixtures, expected outputs, negative cases and boundaries; separating document-checkable checks from runtime-only checks; separating backup creation from tested restore; marking hosting, stack choice, staleness window and ESI encryption as unresolved proposals.

Limitations: no GitHub, terminal, network or delegation tools are available, so no runtime tests, no live ESI validation, no dependency/asset/game-data licence audit, no upstream identity/version verification, and no board/file-SHA claim verification were possible. All checks are static reading of supplied text only. Word-count aim (1200-1800) is a target, not a rejection gate.

Remaining work / review pending: coordinator review of this draft; owner decisions on staleness window, route weights, stack fork/new-implementation choice, ESI token encryption; dependency/asset/game-data licence checks; runtime execution of WH-T08..WH-T11 after the app exists; independent acceptance before any merge. This specification is a candidate, not accepted or build-ready. No tests were executed and no acceptance is claimed.


## Automated screening
{
  "task_id": "MAP-039",
  "decision": "submit_draft",
  "summary": "MAP-039 draft fully scopes WH-first workflows (scanner paste/preview/diff/save, manual chain editing, stale signatures, jump/mass/life observations, route selection, notes/intel, multi-pilot conflicts, empty/offline/error/denied states), treats mass/life as uncertain, invalidates safety claims on stale holes and unknown activity, specifies route filtering without guessed game constants, defines build sequence WH-B01..WH-B07 and checks WH-T01..WH-T11 with fixtures/expected outputs/negative cases/data-permission boundaries/evidence, separates document-checkable from runtime checks, separates backup creation from tested restore, and lists unresolved blockers. All upstream facts cite pinned Pathfinder/EVE-WHMapper commits/paths/lines; proposed items are labelled proposed. No material defects found; draft is clean for a draft PR, not acceptance.",
  "findings": []
}
