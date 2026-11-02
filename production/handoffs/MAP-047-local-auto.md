# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/41

Automated critic only; independent review pending.

Task: MAP-047 — Research signature, mass and observation evidence boundaries
Worker: hermes-laptop-map-047-auto-20261030
Claim commit (task/claim COMMIT, not token): 783148d08b5c02441f6cd8ab56a1b40ec9ae0780
Output path: docs/map/specs/loop-map-047-wh-research.md (complete substantive file section above, ends with final newline)
Input revisions: baseline 6e023274d7cb692f36b132d980d5a335d4387897 (loop-map-042-wh-design.md); research 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (LOCAL-RESEARCH.md, NEXT-SOURCE-SNAPSHOT.json, next-observations-sources.md)
Sources used: esi/esi-docs 98b42d5 static-data index (receipt sha256 e5ae49a7...); pathfinder 06af7d86 ConnectionModel.php (sha256 6a8ea6f1...); eve-whmapper 2a493fad WHSignature.cs (sha256 9c5a195c...), WHSystemLink.cs (sha256 ff1a7ea8...), import tests (sha256 7cdfe5d4...); ESI metadata compatibility_date 2026-08-18 (openapi receipt sha256 9a9a0f4a..., compatibility-dates sha256 7ac78423..., oauth discovery sha256 dc04adbd...)
Checks actually performed: pinned receipts/hashes recorded; signature field constraints and import fixtures extracted; mass/life representations from both codebases compared; SDE access instructions quoted; ESI selected schema tabled; four distinctions mapped (implementation constant vs game rule, fixture vs format, estimate vs exact mass, known vs unobserved); evidence-status register built; follow-up lookup plan and proposed test cases listed. No MAP-042 §6 examples re-executed; no runtime, server, or authenticated calls.
Limitations: WHJumpLog.cs pinned by baseline but absent from this packet; no SDE build number or changelog content fetched; ESI inventory covers four paths only; root MIT notices do not cover dependencies/assets/game data/CCP agreement; no app exists to execute proposed tests.
Remaining work: owner decisions OD-06 (stale threshold, mass-bucket adoption, route constraints) and OD-11 (signature name max-length); lookup of Config::ESI_GROUP_WORMHOLE_ID and wormhole typeId/massIndividual data; ESI schema revalidation at selected compatibility date before any implementation.
Review pending: coordinator review of this research report. Report is not accepted, does not amend MAP-042, and certifies no implementation, security, compatibility, licence or restore result.


## Automated screening
{
  "task_id": "MAP-047",
  "decision": "submit_draft",
  "summary": "No actionable defects found. The draft correctly addresses OD-06/11: signature field constraints and import fixtures from WHSignature.cs and WHSignatureHelperImportTests.cs; connection mass/life representations from Pathfinder ConnectionModel.php and EVE-WHMapper WHSystemLink.cs; official SDE access instructions from esi-docs static-data index; and the selected ESI schema from public metadata at compatibility date 2026-08-18. It preserves required distinctions (implementation constants vs authoritative game rules, test fixtures vs current formats, estimates vs exact remaining mass, known observations vs unobserved activity), reports WHJumpLog as unavailable evidence, and provides a bounded follow-up lookup plan plus unexecuted stale/conflict/uncertainty test cases. No invented thresholds, safe-route claims, SDE download, or acceptance assertions.",
  "findings": []
}
