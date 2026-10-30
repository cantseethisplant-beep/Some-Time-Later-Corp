# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/10

Automated critic only; independent review pending.

# MAP-005 finished-work handoff

## Task and claim identity
- Task: MAP-005 — Define catalogue entry and evidence fields
- Claim commit: 7e416048cf653d47b0fafae40946fb4a99cf404d
- Worker ID: hermes-laptop-map-005-auto-20261030
- Claim token: qwtgAXv4wOMwdNJM4viqCCxSc_H5gq8H
- Input revision: 792b158838aa5214d0156690d24e21e780de542e
- Run: eve-blueprint-20261030
- Branch: hermes/map-005-auto-20261030

## Output produced
- docs/map/specs/catalogue-entry.md (complete plain-text Markdown specification, no outer wrapper)

## Exact sources used
- README.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/CONCEPT.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/DECISION-GUIDE.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e
- No external sources were consulted; external_research_required is false and runtime_tests_required is false.

## Checks actually performed
- Mapped every acceptance criterion to a schema section: identity/licence/pinned version (4.1), dependency/bundle relationships (4.2), permissions/resources (4.3-4.4), deployment/update/rollback (4.5), backup/restore evidence (4.6).
- Distinguished four entry states with minimum-evidence criteria (section 3) so candidate/documentation-reviewed/component-tested/supported-for-specific-environment are not conflated.
- Separated backup creation fields from restore verification fields throughout section 4.6; restore_verified is never derived from a backup upload.
- Built the section 7 example as synthetic only, with every value marked [synthetic] and a leading statement that the entire block is illustrative; no upstream identity, licence or version was invented.
- Preserved unresolved/open decisions from docs/DECISION-GUIDE.md as unresolved fields rather than mandates.
- Distinguished baseline intent from proposed schema rules (section 2).
- Rephrased the backup-and-restore invalidation trigger in section 6 to reference the existing `acceptable_data_loss_window` field instead of an undefined retention period.

## Limitations
- No GitHub, terminal, network or delegation tools were available; the live board was not re-read and the claim could not be verified against production/board.json.
- No upstream technical verification was performed; the schema contains unresolved values where upstream facts are required.
- No runtime tests were performed.
- The 1200-1800 word target for the specification was aimed at but not machine-verified; the final word count is approximately 2200 words including all sections, tables, and the synthetic example block.

## Remaining work
- Submit the finished-work packet via the project's issue form, linking the original claim issue, with the full file contents.
- Coordinator integration into a work branch and board update to review.
- Owner or appointed reviewer acceptance against MAP-005 acceptance criteria; possible map-index update per docs/PRODUCTION.md.
- Claim release before the worker takes another task.

## Review pending
- The produced specification is a proposal pending coordinator and project-owner review; it is not accepted work.

### Diagnosed issues and exact corrections
1. **Section 7 synthetic unverified example**: The original example contained unmarked values (`hardware_consent_required: true`, `failure_blocks_application: true`, `bundle_role: standalone-application`, `restore_verified: false`, `backup_record: none`) that risked being read as schema defaults or factual assertions, effectively letting an unresolved policy (hardware consent required) become a mandate. Correction: every value in the example is now explicitly marked `[synthetic]`, and the block is preceded by a statement that the entire section is synthetic and illustrative, no value is a default, and no upstream facts have been invented.

2. **Section 6 evidence conditions/invalidation triggers**: The backup-and-restore invalidation trigger cited "the retention period" ("if no restore exercise has succeeded within the retention period"), but no retention period is defined in the inputs or schema, so the trigger cannot be applied as written. Correction: the trigger was rephrased to reference the existing `acceptable_data_loss_window` field ("invalidated if no restore exercise has succeeded within the `acceptable_data_loss_window`") rather than creating or referencing an undefined retention period. The time-window question remains an unresolved decision carried from the baseline.

### Remaining uncertainties
- The specification has not been re-validated against the live production/board.json; claim status against that board is unknown.
- No upstream technical verification was performed; all upstream identity/licence/version fields remain `unresolved` by necessity.
- The word count exceeds the 1200-1800 target due to the detailed invalidation-trigger rationale and the full synthetic example with all values marked.

### Review pending
The produced specification is a proposal pending coordinator and project-owner review; it is not accepted work.


## Automated screening
{
  "task_id": "MAP-005",
  "decision": "submit_draft",
  "summary": "Draft review complete: all prior diagnosed issues are correctly addressed. Section 7 synthetic unverified example now has every value explicitly marked [synthetic] with a leading statement that the entire block is illustrative and no value is a default. Section 6 backup-and-restore invalidation trigger references the existing acceptable_data_loss_window field rather than an undefined retention period. No remaining issues found. Specification maps all acceptance criteria to schema sections, properly distinguishes baseline intent from proposed rules, uses synthetic example with all values marked, and carries unresolved decisions from baseline without mandate.",
  "findings": []
}
