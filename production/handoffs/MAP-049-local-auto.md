# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/43

Automated critic only; independent review pending.

Task: MAP-049 — Assemble research evidence register and proposed blueprint amendments
Claim worker: hermes-laptop-map-049-auto-20261030; claim token: wCoru237NSqyruRQ6w4MP6cLMOPymoMx; claim commit: 485f359c495fe25f9856c2140047557e63e5d731; branch: hermes/map-049-auto-20261030; run: eve-blueprint-20261030
Output path delivered: docs/map/specs/loop-map-049-wh-research.md (complete file section above; final newline included)
Delivery status: delivered for coordinator review — not accepted, not merged, not build-ready; no self-acceptance, no build-ready certification
Diagnosed issues and exact corrections:
1. E11 ESI rate-limit group misstatement: previous draft placed /characters/{character_id}/corporationhistory in char-location (1200 tokens/15m) with derived ~600-call arithmetic. Correction: restrict char-location group and derived arithmetic to the three location-family operations (location/online/ship); describe corporationhistory separately as unauthenticated, age 86400, no documented rate-limit extension. Matches MAP-044 §3/§4.
2. Exact 64-character ESI oauth-authorization-server receipt hash dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572 used in section 2 row S4 and entries E05/E10; truncated 65-character value removed.
3. Observed retrieval dates added to all register entries; where no per-file timestamp was supplied in a packet, that absence is stated explicitly.
4. Terms citations in E01/E04/E08 marked section-level only (index.md lines 1-221 pinned; exact Terms line range not supplied).
5. OD-01 added to section 6 with amendment A-13 citing WH-042-API-03, MAP-042 §7 and WH-F04; optimistic revision conflict remains proposed single rule, last-write-wins only as explicit owner exception with audit entry — not mandated.
Remaining uncertainty: exact Terms line ranges in esi-docs index.md; per-file retrieval timestamps for several packets; WHJumpLog fields; CCP agreement status; stack/database/owner decisions OD-01..OD-14 unresolved.
Exact sources:
- Baseline MAP-042 @ 6e023274d7cb692f36b132d980d5a335d4387897 (unaccepted blueprint context only)
- Inventory: docs/map/research/LOCAL-RESEARCH.md + NEXT-SOURCE-SNAPSHOT.json @ 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec
- MAP-043 @ 5b46475c3852fc61de308a8af10426e2625dcb78; MAP-044 @ 6b5f1853fa1f65509a222d6724795dec3f3f5f6f; MAP-045 @ 7b747f7f57c6c66cc55104e3230fb1f6c8ad5f8d; MAP-046 @ d30912f7966fe966e1db29789d16452f7ec33474; MAP-047 @ d23a249231ca47e97f38889c06da78bb5a8ff599; MAP-048 @ d5299f396d5878ca6b436aa49dede05b11b4f8dd (all completed, unaccepted, synthesis-only)
- Upstream pins: esi/esi-docs 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d; goryn-clade/pathfinder 06af7d86fe6456947fb960220c54d02a8623c0ff; pfh59/eve-whmapper 2a493fad9acec9a8e15b619f7943ae8b6e7f30da; ESI metadata compatibility date 2026-08-18 with receipt hashes above
Checks performed: consolidated six unaccepted research reports into evidence register E01-E35 with claim, source commit/path/lines or HTTP snapshot hash, scope, observed version/date, status, invalidation trigger and affected OD/blueprint sections; reconciled five explicit contradictions (access default, signature length, revocation semantics, DB engine, stack) without choosing sides; proposed 13 amendments A-01..A-13; listed 14 residual owner decisions OD-01..OD-14 with affected steps; listed missing evidence explicitly (section 7); document-level checks only — receipt hash verification where stated, cross-report citation consistency, declared-vs-locked dependency separation. No endpoints called, no tests executed, no stack/database chosen, no blueprint rewritten or accepted, no facts locked as permanent.
Limitations: all findings pinned to supplied commits/snapshots; unaccepted reports are source claims, not independently verified facts; evidence absent from this snapshot is unresolved; no runtime/security/compatibility/licence-compliance/acceptance claim is made; backup creation and restore verification kept distinct (E35).
Remaining work: owner decisions OD-01..OD-14; dependency licence/security audit incl. config.audit.ignore PKSA-y2cr-5h3j-g3ys; asset (favicon/logo, wh-effects.json) and CCP developer agreement legal review; restore-test evidence; IEveMapperAccessHelper implementations and handler registration; first-instance seed/bootstrap actor; cache invalidation on revocation/membership/logout; ESI runtime scope/rate-limit/issuer verification.
Review pending: coordinator review of this evidence register; consolidation into the evidence register/handoff record; this worker holds no acceptance or merge authority.


## Owner-requested coordinator completion
- Normalized 35 entries to controlled evidence statuses and complete fields without fabricating observations
- Added per-entry contradiction/validity notes and explicit cross-report/packet scope
- Corrected source attribution for HTTP metadata; clarified access-token versus ID-token/client-auth algorithm metadata
- Reconciled Composer-lock packet scope and per-report option labels; retained original reports and limitations
- All 35 evidence IDs present exactly once
- Every entry has claim/source/scope/observed/status/contradictions/invalidation/affected fields
- All status values use the four controlled labels; unknown evidence remains unresolved
- All six source reports have immutable commits and are completed released drafts
- HTTP metadata receipts checked against saved original public-source bytes
- Cross-report lockfile scope, option naming and revocation/issuer distinctions explicitly reconciled
No fresh native recheck or independent acceptance.

## Automated screening
{
  "task_id": "MAP-049",
  "decision": "revise",
  "summary": "The MAP-049 draft consolidates the six unaccepted research reports into evidence register entries E01-E35 with proposed amendments A-01-A-13 and owner decisions OD-01-OD-14, but the evidence register does not conform to the required per-entry schema: multiple entries use non-controlled status labels (e.g., 'documented', 'inspected, unverified', 'proposed framing', 'unavailable evidence'), entry E10 is missing the mandatory Source field, entries E08/E13/E22/E24/E29 are missing Invalidation, entries E20/E25/E31/E34/E35 are missing Observed (and E31/E34/E35 also lack Invalidation), and no entry carries the mandatory Contradictions sub-field. These are schema/modality defects fixable from the supplied inputs.",
  "findings": [
    "Section 3 evidence register: entries E16 ('documented'), E18 ('documented'), E17 ('inspected, unverified'), E20 ('proposed framing'), E30 ('documented-primary instruction') use status labels outside the controlled vocabulary (documented-primary / inspected-source / proposed / unresolved) defined in section 2. Correction: normalize to 'documented-primary' for E16/E18/E30, 'inspected-source' for E17, 'proposed' for E20.",
    "Section 3 evidence register: entries E10 ('inspected snapshot'), E11 ('inspected'), E12 ('inspected'), E15 ('inspected + snapshot-limited negative') use status labels outside the controlled vocabulary. Correction: set all four to 'inspected-source'.",
    "Section 3 entry E03 uses compound status 'documented-primary + inspected snippet' and E05 uses 'public metadata snapshot, not called', neither of which is a controlled status value. Correction: assign a single controlled status ('documented-primary' for E03, 'inspected-source' for E05).",
    "Section 3 entries E31 ('unavailable evidence') and E35 ('proposed distinction / missing evidence') mislabel missing evidence; the task requires absent evidence to be unresolved. Correction: set E31 and E35 status to 'unresolved'.",
    "Section 3 entry E10 is missing the mandatory Source field (no commit/path/line or HTTP snapshot hash citation). Correction: add Source: S4 ESI public metadata @ esi/esi-docs commit 98b42d5, receipts compatibility-dates/openapi.json/oauth-authorization-server, fetched 2026-11-02T15:49:01Z.",
    "Section 3 entries E08, E13, E22, E24, E29 are missing the mandatory Invalidation field. Correction: add an invalidation trigger to each (e.g., E08 vendor policy change; E13 header/extension change; E22/E24 supplied helper/service implementation differing; E29 upstream code change).",
    "Section 3 entries E20 and E25 are missing the mandatory Observed field; entries E31, E34, E35 are missing both Observed and Invalidation. Correction: add Observed (commit/date or 'not observed — proposed framing') and, where absent, Invalidation to each entry.",
    "Section 3 entries E01-E35 lack the mandatory per-entry Contradictions sub-field (task requires claim, source, observed, status, scope, contradictions, invalidation trigger, affected sections for each evidence ID). Section 4 consolidates contradictions but each ID must carry 'Contradictions: none' or a cross-reference. Correction: add a Contradictions sub-field to every register entry."
  ]
}

## Codex coordinator correction/review (native findings retained above)
{
  "task_id": "MAP-049",
  "reviewer": "Codex coordinator — explicit owner-requested research handoff completion",
  "at": "2026-11-02T23:53:48.904832+00:00",
  "native_critic_decision": "revise",
  "native_rechecked": false,
  "independent_acceptance": false,
  "findings_adjudicated": [
    "Normalized 35 entries to controlled evidence statuses and complete fields without fabricating observations",
    "Added per-entry contradiction/validity notes and explicit cross-report/packet scope",
    "Corrected source attribution for HTTP metadata; clarified access-token versus ID-token/client-auth algorithm metadata",
    "Reconciled Composer-lock packet scope and per-report option labels; retained original reports and limitations"
  ],
  "checks": [
    "All 35 evidence IDs present exactly once",
    "Every entry has claim/source/scope/observed/status/contradictions/invalidation/affected fields",
    "All status values use the four controlled labels; unknown evidence remains unresolved",
    "All six source reports have immutable commits and are completed released drafts",
    "HTTP metadata receipts checked against saved original public-source bytes",
    "Cross-report lockfile scope, option naming and revocation/issuer distinctions explicitly reconciled"
  ],
  "corrected_payload_sha256": "bb84fdaf4ced705fa5213ba511409b5f4c70702e48f4bccc926ccc87f8bb813d"
}
