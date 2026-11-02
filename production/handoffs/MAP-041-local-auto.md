# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/35

Automated critic only; independent review pending.

Task: MAP-041 — Targeted audit of assembled WH blueprint
Claim commit: a20b1a923aaf4cd495cff0c5671e5215c7b50ba7
Claim worker: hermes-laptop-map-041-auto-20261030
Input revision: 849978908daabe3d2a45f0e758625eedc4bdde30
Output path: docs/map/specs/loop-map-041-wh-audit.md
Status: corrected draft deliverable produced; not accepted; no self-acceptance; no implementation claimed

Diagnosed issues and exact corrections:
1. WH-F05 false cardinality defect — reworded as not-a-defect (Low) and closed. Pathfinder's SystemSignatureModel binds each signature to one systemId with an optional connectionId validated to the same system, and ConnectionModel exposes signatures as has-many navigation from connection; this is compatible with MAP-040 §5 R02 / §6 signature-per-system-with-optional-connectionId design. No inconsistency or reconciliation exists. Deleted residual-unknown cross-reference to WH-F05 (old #12); residual unknowns renumbered to 12 items. Restated section-15 class counts: 11 document-fixable (WH-F01, WH-F03, WH-F04, WH-F06, WH-F07, WH-F10, WH-F12, WH-F13, WH-F14, WH-F15, WH-F16), 3 owner (WH-F02, WH-F08, WH-F11), 1 upstream-evidence (WH-F09), 1 not-a-defect (WH-F05); no ID appears in two classes; all sixteen IDs WH-F01..WH-F16 accounted for.
2. Candidate-section column conflation — every register row now cites an exact MAP-040 section (§3, §5 R01-R10, §6, §8, §9, §10, §11) in the Candidate section column; all MAP-036/037/038/039 references moved into Evidence/source. Verified each row names an existing MAP-040 section: §5 requirements R01-R10, §6 boundaries/API summary, §8 milestones, §9 test matrix, §10 contradictions, §11 missing evidence/blockers.

Remaining uncertainty:
- Target stack (PHP vs C# vs new implementation) owner-undecided; PHP/C# internals must not be combined by assertion.
- ESI scopes, rate limits, issuer contract, consent workflow, token revocation effectiveness unverified upstream-evidence blocks (WH-F09, WH-F11, WH-F13).
- Full dependency licence/security audit for both manifests, asset licence checks, EVE game-data/ESI terms missing (WH-F15).
- Restore-test evidence missing; backup creation is not restore verification (WH-F07, WH-F16).
- Concurrent-edit rule (optimistic revision vs last-write-wins) unresolved pending owner decision or single stated rule (WH-F04).
- Signature name max-length, mass-bucket mapping, stale threshold, route weights, database engine, bootstrap actor designation unresolved (WH-F03, WH-F14, WH-F02, WH-F08, WH-F16, WH-F06).

Checks actually performed:
- Single-pass audit of candidate vs MAP-036..MAP-039, WH-FIRST-BRIEF, and pinned Pathfinder/EVE-WHMapper extracts at input revision 849978908daabe3d2a45f0e758625eedc4bdde30.
- Stable finding register WH-F01..WH-F16 with severity, blocker class, candidate section, evidence/source, issue, correction, verification procedure.
- All four MAP-037 §7 examples checked against declared fields, ID format, tenant scope, error definitions; structural pass (one conditional on shipMass type via WH-F10).
- Schema/example/type/ID consistency, duplicate signature rules, concurrent/delete/stale handling, authorization reads/writes/events, cross-map isolation, consent/revocation/cache privacy, routing/exact-mass claims, MIT attribution, dependency inventory, import/export/migration, backup vs restore, WH-first vs cloud scope.
- Coverage matrix built for all audited areas.
- Residual unknowns enumerated (12 items after WH-F05 removal).
- No runtime tests executed; no live ESI access; no dependency/security audit performed.

Limitations:
- Supplied text only; no GitHub, terminal, network, or delegation tools.
- No runtime verification of upstream extracts; no executed scripts or test runs.
- Unaccepted designs treated as evidence only, not accepted requirements or technical evidence.
- README claims distinguished from inspected implementation; no upstream instruction followed.
- Word-count aim (1200–1800 words) not verified against final output length.

Remaining work / review pending:
- Owner decisions required: stack selection, explicit-grant-only vs permissive access-list default, opt-in tracking default/expiry, numeric stale threshold/mass buckets/route weights, bootstrap actor designation, signature name max-length.
- Upstream-evidence blocks: full dependency licence/security audit for both manifests, asset licence checks, EVE game data/ESI terms-of-use, ESI scopes/rate limits/issuer contract, token revocation effectiveness, encrypted-at-rest adoption decision.
- Document fixes to apply (coordinator/owner approval): resolve concurrent-edit contradiction (WH-F04), separate instance/bootstrap ops from MVP API (WH-F01), declare shipMass type (WH-F10), restore vs backup distinction (WH-F07), mark DB engine undecided (WH-F16), add import remapping table (WH-F12), label consent model proposed (WH-F13), mark JUMP_MASS_BUCKETS not adopted (WH-F14).
- Independent acceptance and technical evidence still required before any build-ready claim. No task repetition, no generic global audit, no security certification claimed.


## Automated screening
{
  "task_id": "MAP-041",
  "decision": "submit_draft",
  "summary": "No current defects found in the MAP-041 audit draft. The finding register WH-F01 through WH-F16 is complete: each row has severity, blocker class, exact MAP-040 section, pinned source citation, issue, correction, and verification procedure. All four inherited MAP-037 section-7 examples were checked against declared fields, ID format, tenant scope, and error definitions (three pass, one conditional on the shipMass type clarification in WH-F10). The coverage matrix, 12 residual unknowns, WH-first scope preservation, unaccepted-proposal labeling, optional cloud scope, and backup-versus-restore distinction are all present. No invented tests or approvals.",
  "findings": []
}
