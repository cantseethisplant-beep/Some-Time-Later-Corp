# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/16

Automated critic only; independent review pending.

MAP-019 evidence categorization and validation workflow — proposed follow-up draft produced.

Claim commit: c1e74a892cc10141ee103f99b359465d1381f678; claim worker: hermes-laptop-map-019-auto-20261030; loop policy 1 / kind followup / cycle 1 / area upstream-evidence / key gap-key-upstream-001.

Output path: docs/map/specs/loop-map-019-followup.md (complete file section returned above, with a final newline).

Exact sources used: all nine input revisions declared in the task contract — baseline revision 792b158838aa5214d0156690d24e21e780de542e (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md) and unaccepted completed drafts MAP-001 through MAP-011 at their declared revisions. No other sources consulted; no external research, network, terminal, GitHub, or implementation access used.

Diagnosed issues and exact corrections:
- Section 2, four epistemic states prose: the baseline revision hash had trailing punctuation appended to the exact 40-character SHA. Corrected to the bare hash 792b158838aa5214d0156690d24e21e780de542e wherever cited as an exact revision.
- Required field comparison against examples: EV-DOC-019-001 populates all required provenance fields (record_id, evidence_category, source_file, source_revision, source_section, environment, check_date, check_method, result, limitations, invalidation_triggers, affected_records, status) plus review fields (reviewer, review_method, criteria_checked). EV-DOC-019-002 marks unreviewed fields as not performed/unresolved rather than inventing values. Component-tested and integration-tested templates mark component_identity, restore_verified, components_involved, interface_checked, fencing_behaviour as unresolved/not performed.
- Unresolved policy not mandated: retention targets, recovery targets, key storage, custodian succession, stack/provider/licence remain unresolved and are not adopted as defaults or mandates in examples. New schema choices (five categories, provenance template, invalidation triggers, affected_records) are labeled proposed design, distinct from baseline user intent.

Checks actually performed:
- Inventoried inputs and evidence types; separated four epistemic states (baseline intent, proposed design, unaccepted drafts, verified evidence).
- Defined five distinct evidence categories with modality preserved ("may"/"should"/"must" not collapsed).
- Populated a documentation-reviewed template with all required provenance fields (synthetic illustrative example EV-DOC-019-001 plus unresolved template EV-DOC-019-002).
- Documented per-category invalidation triggers with operationalization (reopen only affected records; status → reopened).
- Verified progression path from intent to component-tested with all test templates marked not performed; backup creation and restore verification kept distinct.
- Mapped all six MAP-019 acceptance criteria to sections.
- Left proposed actions unapproved with owners/dates unresolved.

Limitations:
- Claim confirmation could not be independently verified (no GitHub access).
- All component-tested and integration-tested records are marked "not performed"; no tested capability is claimed.
- Unaccepted drafts were treated strictly as review material, not accepted requirements or evidence.
- No external write performed; no branch, submission, or acceptance asserted.

Remaining work:
- Coordinator claim verification and release.
- Independent reviewer completion of proposed actions 1–3.
- Independent acceptance of this draft.
- Reconciliation of any contradictions among MAP-001–MAP-011 drafts to be resolved by the reviewer, not by this worker.

Review pending:
- Full specification text, template field completeness against required provenance fields, invalidation trigger patterns, and the acceptance-criteria mapping.



## Automated screening
{
  "task_id": "MAP-019",
  "decision": "submit_draft",
  "summary": "The draft satisfies all six MAP-019 acceptance criteria with no findings. Section 4 defines the documentation-reviewed template and populates every required provenance field plus reviewer/review_method/criteria_checked in synthetic example EV-DOC-019-001, while EV-DOC-019-002 preserves unperformed checks as not performed/unresolved instead of inventing values. Section 6 documents operationalized invalidation triggers for all five evidence categories with reopen-only-affected-records behavior. Section 3 keeps the five categories distinct and preserves may/should/must modality. Section 5 shows the intent to component-tested progression with every test template marked not performed, and backup creation stays separate from restore verification. Section 8 disclaims any tested capability, and Section 2 explicitly distinguishes baseline intent, proposed design, completed unaccepted reference drafts, and genuinely verified evidence (none exists). All source revisions match the pinned task contract; no unsupported claims, contradictions, or mandatory-vs-example violations were found.",
  "findings": []
}
