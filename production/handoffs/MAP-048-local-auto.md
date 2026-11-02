# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/42

Automated critic only; independent review pending.

# MAP-048 Handoff

**Task:** MAP-048 — Research fork versus new-code and database options  
**Claim commit (tracked, not token):** c939860ec0a673a7175a0286b3721644e16e963b  
**Worker:** hermes-laptop-map-048-auto-20261030  
**Delivered output:** docs/map/specs/loop-map-048-wh-research.md (complete file section above)  
**Status:** Submitted for coordinator review — not accepted, not build-ready, no implementation performed

## Inputs used
- Baseline revision 6e023274d7cb692f36b132d980d5a335d4387897 — docs/map/specs/loop-map-042-wh-design.md (completed UNACCEPTED blueprint context; evidence for OD-02/OD-12, fork options A/B/C, backup ≠ restore distinction)
- Inventory revision 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec — docs/map/research/LOCAL-RESEARCH.md and docs/map/research/NEXT-SOURCE-SNAPSHOT.json (local research policy; snapshot pin registry)
- Options revision 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec — docs/map/research/next-options-sources.md (pinned primary source text: Pathfinder and EVE-WHMapper LICENSE/README/composer.json/WHMapper.csproj/docker-compose.yml with receipt hashes)

## Checks actually performed
- Source-pin inventory across both upstream projects at pinned commits; recorded receipt SHA256 values where supplied.
- Separated README-claimed features (unverified) from manifest/deploy code facts (inspected).
- Compared database assumptions: unnamed ext-pdo generic (Pathfinder) vs PostgreSQL via Npgsql/EF Core + postgres:17 compose (WHMapper).
- Inventoried dependency evidence gaps: absent composer.lock, audit-ignore entry, 10.* version ranges, transitive licences, asset licences.
- Verified backup/restore distinction: no restore-test evidence in either packet; backup creation ≠ restore verification.
- Cross-checked against MAP-042 OD-02 (stack decision) and OD-12 (DB engine), WH-F16 (DB undecided, compose example only).

## Limitations
- No network, shell, account, delegation or server tools; source packets are the only research available.
- No runtime tests executed; no README feature claim verified as behavior.
- No licence compliance, security, compatibility or performance determination made.
- composer.lock and transitive dependency sets unavailable; lockfile absence means dependency surface unpinned for Pathfinder.
- No restore-test, migration-execution, or asset/CCP-agreement evidence exists in the inputs.
- esi/esi-docs is pinned in the snapshot registry but no esi-docs document was supplied to this task.

## Remaining work
- Owner decisions OD-02 (language/runtime/stack) and OD-12 (database engine).
- Dependency licence audit for the chosen manifest; asset licence review (favicon/logo or wh-effects.json); EVE game data/ESI terms and CCP developer agreement review.
- Restore-test evidence and migration evidence for the chosen database.
- Coordinator review of this report before any downstream use as input.

## Review pending
Coordinator review of docs/map/specs/loop-map-048-wh-research.md against MAP-048 acceptance criteria. No self-acceptance claimed; no branch, submission or acceptance performed by this worker.


## Automated screening
{
  "task_id": "MAP-048",
  "decision": "submit_draft",
  "summary": "No current actionable defects. The draft accurately compares Pathfinder fork, WHMapper fork and new implementation using the pinned manifests/README/deployment examples; separates README-claimed features (documented, not verified) from inspected code facts; keeps backup creation distinct from restore verification and baseline intent distinct from proposed rules; documents dependency, asset, legal and restore-test gaps plus the full missing-evidence register; addresses OD-02 and OD-12 with explicit decision criteria without selecting a stack, promising savings, determining licence compliance, or claiming performance/compatibility tests; evidence status, versions/pins and what invalidates findings are stated throughout.",
  "findings": []
}
