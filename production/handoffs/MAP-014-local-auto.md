# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/12

Automated critic only; independent review pending.

MAP-014 | hermes-laptop-map-014-auto-20261030 | claim commit 785043b757e72e9033c8f5595c6a303f724a5297

Task: Define node enrolment and withdrawal lifecycle
Claim token: I8oVCKI5212yw99yMOML3ZyayV5zdKRG
Input revision: 792b158838aa5214d0156690d24e21e780de542e
Output path: docs/map/specs/node-lifecycle.md

Sources checked:
- README.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/CONCEPT.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/DECISION-GUIDE.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e

Checks performed:
- All eight lifecycle states (offered, enrolment-pending, approved, active, disconnected, draining, revoked, retired) defined with meanings traceable to source documents.
- Distinction between management-access removal and verified workload/data cleanup on offline physical host explicitly preserved; no claim of isolation from hardware owner.
- Unresolved decisions identified and preserved as unresolved (identity/key mechanism, offline withdrawal procedure, recovery custodian separation, OS/runtime/cloud scope).
- No upstream technical verification, licences, tests, implementation, costs, or chosen stack invented.
- Trust evidence requirements extracted and recorded; actual verification deferred.
- Acceptance criteria against MAP-014 scope satisfied; scope boundaries respected (resource offer fields remain with MAP-003).

Limitations:
- No GitHub write access; document produced in chat.
- No upstream technical verification performed; baseline is user-intent only.
- Unresolved policy decisions left as open; not claimed as mandates.
- Two document corrections and six model-request attempts bounded per task constraints.

Remaining work:
- Resolution of unresolved identity/key mechanism (must not invent).
- Procedure for offline hardware owner withdrawal (open per DECISION-GUIDE.md).
- Backup/restore evidence per application bundle.
- Recovery custodian separation rules.
- Integration and acceptance gate follow-up.



## Automated screening
{
  "task_id": "MAP-014",
  "decision": "submit_draft",
  "summary": "Draft MAP-014/node-lifecycle meets all acceptance criteria: all 8 lifecycle states defined with source-traceable meanings (Section 2); management-access removal vs. verified workload/data cleanup distinctly preserved in Section 6; trust evidence and unresolved identity/key mechanism identified in Section 5 without claiming hardware owner isolation. No issues from supplied inputs require revision.",
  "findings": []
}
