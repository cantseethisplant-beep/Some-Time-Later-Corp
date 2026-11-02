# WH blueprint — start here

Completed planning/review candidate. Not accepted, implemented, runtime-tested or certified build-ready.
Project: Some Time Later Corp / Eve Cloud. Creator: VelesPhylakos. Core: WH mapping/intel/operations; cloud hosting is optional.

## Reading order

1. Read [the corrected consolidated blueprint](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6e023274d7cb692f36b132d980d5a335d4387897/docs/map/specs/loop-map-042-wh-design.md), especially section 15 (OD-01..OD-14), section 9 (ordered build plan), section 7 (contracts), section 10 (tests/traceability), and section 12 (audit disposition).
2. Read [the targeted integration audit](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/fa913fc258b0b459e57499220ef31476a6f392bc/docs/map/specs/loop-map-041-wh-audit.md) alongside the final disposition table. Original issues remain auditable; unresolved entries are not silently accepted.
3. Use the four component documents below for detail. The final blueprint states proposed reconciliations where those independent drafts disagree.
4. Use [package-manifest.json](WH-BLUEPRINT-MANIFEST.json) for immutable public commits and SHA-256; evidence/ includes the original pinned brief and both source packs with MIT notices. The evidence brief is the historical task-input snapshot, not the later operational recovery policy.

## Package contents

- [1. MAP-036](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/abedc17bddc7f573f434f4dad78969471b9f3c9e/docs/map/specs/loop-map-036-wh-design.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/32
- [2. MAP-037](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/fb2bb57a8f28f5362912f6c4a94d5845dbaabd2a/docs/map/specs/loop-map-037-wh-design.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/33
- [3. MAP-038](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/d68d560c9f6687f96bf82de8a980b13c385a7f2b/docs/map/specs/loop-map-038-wh-design.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/30
- [4. MAP-039](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/556f3f983f9b1d3b2b3acc20853bcfd18c797348/docs/map/specs/loop-map-039-wh-design.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/31
- [5. MAP-040](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/3b106a956ed936af87f80ffcc293741ebf9303bc/docs/map/specs/loop-map-040-wh-design.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/34
- [6. MAP-041](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/fa913fc258b0b459e57499220ef31476a6f392bc/docs/map/specs/loop-map-041-wh-audit.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/35
- [7. MAP-042](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/6e023274d7cb692f36b132d980d5a335d4387897/docs/map/specs/loop-map-042-wh-design.md) — https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/36

## What the next builder can do

Use B00 to record the stack, bootstrap and applicable access/consent choices. Follow B01 → B05 → B02/B03/B04 → B06 → B07 with the explicit prerequisites. Before identity/security prerequisites are resolved, use isolated synthetic fixtures only. Do not use real tokens or player data or deploy a partially protected service.
Trace each WH-042-R requirement to its build steps and observable tests in section 10. Distinguish checking a specification from running an implementation test. Preserve source notices and verify only the precise upstream/dependency/API/runtime evidence required by the affected step.
OD-01..14 identify concurrent-edit exception policy; stack; ESI contract/scopes; dependency licence/security review; asset/game-data terms; numerical uncertainty policies; token/revocation implementation; tested restore evidence; handler authorization evidence; initial-owner bootstrap; signature length; database engine; permission defaults; and opt-in/expiry choices. Several are future evidence tasks, not questions the owner can answer by declaration.
After decisions/evidence are recorded, an independent reviewer must accept a frozen revision before treating the candidate as an agreed build baseline. No app implementation or deployment was performed by this planning run.

## Review provenance

MAP-036 passed a fresh native critic. MAP-037 has a disclosed narrowly checked example-key repair without native recheck. MAP-042 has explicit owner-requested Codex corrections/review without native recheck. All are draft proposals; original native reports and raw hashes are retained in the local worker history and correction details are disclosed in the PRs.
The run used free-only Hermes routes. Completing this package spent zero further inference requests; original request counters are unchanged. No drafts were merged or independently accepted.
