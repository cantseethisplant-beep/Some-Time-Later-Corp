# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/21

Automated critic only; independent review pending.

# MAP-026 Handoff — Node Enrolment Gate and Restore-Proof Evidence

**Task / claim**: MAP-026 — Reconcile the node enrolment gate with restore-proof evidence (MAP-014 section 5 vs MAP-004 sections 5 and 8)
**Commit**: 84f33db7dc5cade0e9f0739d5a2d40341852eeb1 (claim commit; not a token)
**Worker**: hermes-laptop-map-026-auto-20261030
**Input revision**: 792b158838aa5214d0156690d24e21e780de542e
**Output path**: docs/map/specs/loop-map-026-followup.md
**Status**: drafted for review; not accepted; no submission performed

## Exact sources used
- README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e — user-intent baseline; no upstream technical verification.
- docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210 — MAP-014 draft (unaccepted review material); section 5 disputed passage quoted.
- docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca — MAP-004 draft (unaccepted review material); sections 5 and 8 quoted.
- docs/map/specs/loop-map-023-followup.md @ 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 — MAP-023 proposed replacement wording (section 4) adopted as proposed design only.

## Checks actually performed
- Quoted baseline "Backup and movement" passages from TRUST-AND-RECOVERY.md and confirmed baseline does not prescribe restore-before-approval or lifecycle placement of restore evidence.
- Quoted MAP-014 section 5 and confirmed it lists a tested restore exercise as required before offered→approved, presented as baseline-derived without proposed-design labelling.
- Quoted MAP-004 sections 5 and 8 and confirmed result categories (attempted, succeeded, failed, not performed) and the no-restore-test-performed statement.
- Adopted MAP-023 section 4 replacement wording: enrolment prerequisites = hardware owner consent, application reviewed immutable version, measured resources; restore-proof separated as assignment-readiness/owner-policy and explicitly proposed.
- Preserved backup integrity vs restore verification distinction (MAP-004 §2, §5).
- Modality crosswalk completed; no may/should/must collapsed; unresolved owner policy left unresolved.

## Limitations
- No GitHub, terminal, network or delegation tools available; board state and file SHAs not independently verified.
- All referenced drafts are unaccepted completed drafts for review only; not accepted requirements or technical evidence.
- No restore test, component test, or integration test performed or claimed.
- No policy choice made (restore-gating timing, decryption authority, offline-host withdrawal).
- This document is a reconciliation proposal only; acceptance rests with project owner or appointed reviewer.

## Remaining work
- Coordinator/owner review of docs/map/specs/loop-map-026-followup.md.
- Up to two document corrections may apply under task policy.
- Acceptance and any merge remain with the project owner or appointed reviewer; claim release required before another task.
- No self-acceptance; nothing in this handoff is implementation evidence.

## Review pending
Yes — this draft is review input only.


## Automated screening
{
  "task_id": "MAP-026",
  "decision": "submit_draft",
  "summary": "The draft satisfies all three acceptance criteria: replacement section 5 lists enrolment prerequisites (hardware owner consent, application reviewed immutable version, measured resources) and excludes restore-before-approval from baseline claims, labelling any restore-gating policy as proposed design with citations to docs/TRUST-AND-RECOVERY.md and docs/map/specs/backup-recovery.md sections 5 and 8; restore-exercise result categories (attempted, succeeded, failed, not performed) and the no-restore-test-performed statement are retained via the MAP-004 cross-reference, with backup integrity and restore verification kept distinct; baseline intent, proposed design, completed unaccepted reference drafts, and genuinely verified evidence are explicitly separated throughout sections 1, 4, 6, and 7. No unsupported tests, implementation, external research, or resolved owner policy are introduced; unresolved choices remain marked unresolved.",
  "findings": []
}
