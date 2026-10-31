# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/18

Automated critic only; independent review pending.

# MAP-023 Handoff

Task: MAP-023 — Reconcile node approval and restore-proof requirements
Claim worker: hermes-laptop-map-023-auto-20261030
Claim commit: b960635fbfd0464f76c87f5cab36ad13ab9989cc
Claimed branch (not created by this worker): hermes/map-023-auto-20261030
Loop: policy 1, kind follow-up, cycle 2, area node-security, key node-approval-restore-proof-boundary

Output path: docs/map/specs/loop-map-023-followup.md

Exact sources:
- README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e (user-intent baseline; no upstream technical verification)
- docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210 (MAP-014 draft, section 5 in scope)
- docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca (MAP-004 draft, sections 5 and 8 in scope)

Checks actually performed:
- Inventoryed all pinned inputs at exact revisions; classified each as baseline or unaccepted completed draft for review only.
- Quoted conflicting passages: TRUST-AND-RECOVERY baseline restore statement; MAP-014 §5 enrolment-gate list including "tested restore exercise must exist ... before a node may transition from offered to approved"; MAP-004 §5 restore-evidence evidence list with result categories attempted/succeeded/failed/not performed; MAP-004 §8 no-restore-test-claimed limitation.
- Compared baseline intent (restore exercise proves recoverability; not an enrolment gate) with the MAP-014 §5 disputed restore-before-approval gate.
- Produced proposed replacement wording for MAP-014 §5 separating node enrolment/approval, assignment readiness, and demonstrated recoverability.
- Built source/modality crosswalk: restore-before-node-approval explicitly labelled proposed or removed as a claimed baseline gate; restore-exercise requirement for proof of recoverability retained intact.
- Verified distinctions: enrolment vs assignment authorisation vs backup integrity vs demonstrated recoverability; all test evidence reported as unverified/not performed; owner policy decisions left unresolved.
- Distinguished baseline intent, proposed design, completed unaccepted reference drafts, and genuinely verified evidence (none).

Limitations:
- No GitHub, terminal, network or delegation tools; board state and file SHAs not independently verified.
- No upstream technical verification, software licence, test, implementation detail, cost, or chosen stack claimed or invented.
- All draft inputs remain unaccepted review material; no accepted requirement changed.
- No restore test performed or claimed.

Remaining work:
- Coordinator or project-owner review of this draft; up to two document corrections may apply under task policy.
- Acceptance and any merge remain with the project owner or an appointed reviewer; nothing self-accepted.

Review pending: yes.


## Automated screening
{
  "task_id": "MAP-023",
  "decision": "submit_draft",
  "summary": "MAP-023 draft is complete and compliant with the task contract. It cites exact revisions and sections: baseline README/CONCEPT/DECISION-GUIDE/TRUST-AND-RECOVERY @ 792b1588..., MAP-014 docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210 section 5, and MAP-004 docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca sections 5 and 8. It quotes the conflicting passages (baseline \"a restore exercise is required\" vs MAP-014 §5 listing \"tested restore exercise must exist\" among items required before offered→approved) and provides proposed replacement wording separating node enrolment/approval, assignment readiness, and demonstrated recoverability. Restore-before-node-approval is explicitly labelled proposed design and removed as a claimed baseline gate, while the restore-exercise proof-of-recoverability requirement remains intact. Backup integrity is kept distinct from restore verification, all test evidence is reported as not performed/unverified, owner policy is left unresolved, and baseline intent, proposed design, unaccepted reference drafts, and verified evidence (none) are explicitly separated. No unsupported facts, implementation claims, or out-of-scope policy choices found.",
  "findings": []
}
