# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/11

Automated critic only; independent review pending.

MAP-011 evidence-record specification — draft for coordinator review

Task: MAP-011 "Define map-wide evidence and invalidation records"
Claim commit (repository working tree): 20706f1095cf9774998548660e36e2ab6be0debc
Pinned input revision: 792b158838aa5214d0156690d24e21e780de542e
Worker: hermes-laptop-map-011-auto-20261030
Output path: docs/map/specs/evidence-record.md (complete file section delivered above)
Status: draft — not self-accepted; submission and acceptance pending coordinator review

Exact sources used:
- README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md, all @ 792b158838aa5214d0156690d24e21e780de542e (user-intent baseline; no upstream technical verification)

Checks actually performed:
- Inventoried the four pinned inputs and confirmed they match the declared task inputs at the declared revision.
- Mapped each MAP-011 acceptance criterion to spec sections: five separated evidence categories (section 1); common provenance schema covering exact source/revision, environment, check date/method, result, limitations, invalidation triggers and affected records (section 2); category-specific additions (section 3); baseline intent separated from proposed schema rules, with unresolved policies excluded from mandates and examples (section 4); synthetic examples verified so none asserts a tested component and backup/restore remain distinct (section 5); targeted reopening rules (section 6); validity, reuse and stated limitations (section 7).
- Verified examples against required fields: all examples carry record_id, evidence_category, source_file, source_revision, source_section, environment, check_date, check_method, result, limitations, invalidation_triggers, affected_records and status; all are marked synthetic; none names a real upstream component, licence, cost or stack; none claims any component or integration test; restore_verified is false wherever backups are mentioned; unresolved policies (spending limits, custodian succession, provider, OS/runtime, RTO/RPO, licensing) appear only as open items, never as mandates in examples.

Limitations:
- No GitHub, terminal, network or delegation tools are available; live production/board.json, production/HERMES-PROGRESS.md and linked handoffs could not be re-read, and the claim confirmation could not be independently verified against the board.
- No technical verification, testing, restore exercises or cost research was performed; all such evidence remains absent by design.
- Synthetic examples are illustrative only and are not evidence.

Remaining work:
- Coordinator review of this deliverable against the MAP-011 acceptance criteria; possible corrections and return to the claimed state.
- Coordinator claim release before this worker takes any other task.
- MAP-005 application catalogue fields remain out of scope.
- Actual component, integration and restore testing belongs to later map tasks, not this one.

Review pending: yes — this handoff and the spec above await coordinator review and an acceptance decision.


## Automated screening
{
  "task_id": "MAP-011",
  "decision": "submit_draft",
  "summary": "The draft evidence-record.md specification meets all MAP-011 acceptance criteria. It separates five evidence categories (user intent, proposed design, documentation-reviewed, component-tested, integration-tested) with proper provenance schemas. Synthetic examples are clearly marked and never assert tested components or real upstream identities. The common provenance schema includes all required fields (record_id, source_file, source_revision, source_section, environment, check_date, check_method, result, limitations, invalidation_triggers, affected_records, status). Baseline intent is separated from proposed schema rules, and unresolved policies (spending limits, recovery custodian succession, chosen provider, OS/runtime, RTO/RPO, licensing) are deliberately not mandated in examples. Targeted reopening rules correctly affect only affected records without converting unresolved policies into mandates. The specification honestly states limitations: no technical verification was performed, inputs are user-intent baseline only, and backup creation remains distinct from restore verification. All acceptance criteria are satisfied.",
  "findings": []
}
