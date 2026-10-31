# Evidence Categorization and Validation Workflow — MAP-019

**Task:** MAP-019 — Establish evidence categorization and validation workflow
**Claim commit:** c1e74a892cc10141ee103f99b359465d1381f678
**Claim worker:** hermes-laptop-map-019-auto-20261030
**Loop:** policy 1, kind followup, cycle 1, area upstream-evidence, key gap-key-upstream-001
**Output path:** docs/map/specs/loop-map-019-followup.md
**Status:** proposed follow-up draft for review; not accepted work. This repository is concept and planning only; no component, integration, restore, or cost claim has been technically verified.

## 1. Purpose and scope

This specification defines a practical workflow for advancing evidence from user intent toward component testing, and template records for documentation-reviewed checks. It is produced under the bounded follow-up rules: review and reconciliation only. Completed drafts referenced as inputs are unaccepted review material, not accepted requirements or technical evidence.

Scope:
- Define five evidence categories and keep them distinct; never collapse user intent, proposed design, documentation review, component test, or integration test into one label or status.
- Provide a documentation-reviewed template with all required provenance fields populated: reviewer, date, method, and criteria_checked.
- Establish invalidation trigger patterns per category that can be operationalized (status change to reopened, re-evaluation of affected records).
- Show the progression path from intent to component-tested using synthetic templates only; no test is claimed performed.
- Preserve every unresolved choice, evidence limit, and exact source provenance from the inputs.

Out of scope: selecting a stack, provider, licence, cost, or runtime; performing any backup, restore, component, or integration test; treating any draft as accepted.

## 2. Source inventory and evidence status

| Revision | Paths | Evidence type |
|---|---|---|
| 792b158838aa5214d0156690d24e21e780de542e | README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md | User-intent baseline; no upstream technical verification |
| c6cc2de20805455eb55c0343394d01225ff41ffd | docs/map/specs/requirements.md (MAP-001) | Unaccepted completed draft for review only |
| 3585afed129ad2694660fcee8cfd982092551117 | docs/map/specs/permissions.md (MAP-002) | Unaccepted completed draft for review only |
| 0e60848ccbfa295169422eab063f1b81023b390e | docs/map/specs/hosting-assignment.md (MAP-003) | Unaccepted completed draft for review only |
| ccf0957af0d80fe4608fc08b06b02408b485b1ca | docs/map/specs/backup-recovery.md (MAP-004) | Unaccepted completed draft for review only |
| 96464d45c5c79db31a82bcb9cf13a1b1b65fb141 | docs/map/specs/catalogue-entry.md (MAP-005) | Unaccepted completed draft for review only |
| 111a5832102570811dd0af21fffd16a70413febc | docs/map/specs/operations.md (MAP-006) | Unaccepted completed draft for review only |
| 9f330ee125a04bdd6f5df1338b38c93ff2fe0162 | docs/map/specs/scheduling.md (MAP-007) | Unaccepted completed draft for review only |
| 119bb89f6decab9c887e0e99bde38e7d6b1a6744 | docs/map/specs/evidence-record.md (MAP-011) | Unaccepted completed draft for review only |

Four epistemic states are kept separate throughout:
1. Baseline intent — the four pinned concept documents at revision 792b158838aa5214d0156690d24e21e780de542e. These state product intent, not technical evidence.
2. Proposed design — new schema and workflow rules proposed in this and related draft files; pending separate acceptance.
3. Completed unaccepted reference drafts — MAP-001 through MAP-011 drafts listed above; usable for contradiction finding and reconciliation, not for dependency satisfaction.
4. Genuinely verified evidence — none exists in this map. Every component-tested and integration-tested template below is marked not performed.

## 3. Five evidence categories (kept distinct)

| Category | Meaning | Proves | Does not prove | Modality note |
|---|---|---|---|---|
| User intent | What the corporation wants, from the pinned concept documents. | Stated product intent. | Compatibility, capacity, or that anything works. | "must" here expresses intent, not implemented behaviour. |
| Proposed design | New schema, template, and workflow rules proposed by map tasks. | A design exists on paper. | That the design works or is accepted. | Proposals are not mandates until accepted. |
| Documentation-reviewed | A record checked against acceptance criteria by documentation review. Reviewer, date, method, criteria_checked recorded. | The document text was reviewed against stated criteria. | Running software, a restore, or a measured result. | Result concerns document text only. |
| Component-tested | A measured check of one component in a stated environment. | One observed component behaviour with date, environment, outcome. | Integration behaviour, fencing, or deployment safety. | Not asserted for any component in this map. |
| Integration-tested | A measured check of two or more components together, including interfaces and fencing where movement is involved. | Observed multi-component behaviour. | That the system is safe to deploy at scale. | No integration is asserted in this map. |

Categories are stored in the `evidence_category` field and must never be merged into a single flag. A GitHub listing, a documentation review, or a backup record alone qualifies as none of the tested categories. Backup creation and restore verification are distinct evidence items; a successful backup record is never accepted as restore verification.

## 4. Documentation-reviewed template

Every documentation-reviewed record carries the full common provenance set plus review-specific fields. Required provenance fields:

- record_id — stable identifier (e.g., EV-DOC-019-001).
- evidence_category — documentation-reviewed.
- source_file — exact repository path.
- source_revision — exact git revision of the source.
- source_section — heading or anchor used.
- environment — where the check occurred; for document review, the repository path is the environment.
- check_date — ISO-8601 date, or "not performed".
- check_method — how the result was obtained (e.g., documentation review — checklist walkthrough, acceptance-criteria comparison).
- result — pass, flag, fail, unresolved, or not performed.
- limitations — what the result does not cover.
- invalidation_triggers — concrete changes that void the record.
- affected_records — record IDs that must be re-evaluated when this record is invalidated or reopened.
- status — valid, superseded, reopened, or unresolved.
- reviewer — person or role who performed the review (synthetic reviewers are marked illustrative).
- review_method — checklist walkthrough, consistency cross-check, acceptance-criteria comparison.
- criteria_checked — list of acceptance criteria examined.

Optional fields are included only when known: proposal_date, measured_values, related_records, remediation, next_check_due. Unknown values are never invented.

### 4.1 Populated template example (synthetic, illustrative only)

- record_id: EV-DOC-019-001
- evidence_category: documentation-reviewed
- source_file: docs/map/specs/backup-recovery.md
- source_revision: ccf0957af0d80fe4608fc08b06b02408b485b1ca
- source_section: Section 2 — Outcome labels by record concept
- environment: repository text review; no host or component involved
- check_date: 2026-10-31
- check_method: documentation review — acceptance-criteria comparison against MAP-019 criteria and baseline inputs
- criteria_checked: separate requested/running/verified copy/failed/restore-tested outcomes; unresolved values listed (custodian access, key separation, offline hosts, retention, targets); no completed restore tests claimed
- result: flag — draft preserves backup/restore distinction and lists unresolved values; no technical verification of any backup behaviour
- limitations: reviews draft text only; not a restore test, not component evidence, not acceptance of the draft
- invalidation_triggers: backup-recovery.md revision change; MAP-019 acceptance criteria change; contradiction with an accepted record
- affected_records: EV-COMP-* restore records citing this section; EV-INT-* movement records
- status: valid
- reviewer: synthetic reviewer (illustration only)
- review_method: acceptance-criteria comparison

### 4.2 Unresolved template (no check performed)

- record_id: EV-DOC-019-002
- evidence_category: documentation-reviewed
- source_file: docs/map/specs/requirements.md
- source_revision: c6cc2de20805455eb55c0343394d01225ff41ffd
- source_section: Section "Requirements" table, REQ-05 through REQ-17
- environment: not performed
- check_date: not performed
- check_method: not performed
- result: not performed
- limitations: no review executed; draft status unaccepted
- invalidation_triggers: not determined until review occurs
- affected_records: not determined
- status: unresolved
- reviewer: unresolved
- review_method: unresolved
- criteria_checked: unresolved

## 5. Progression path: intent to component-tested

Templates show how a single topic advances. Each step keeps its own category; a later category never retroactively re-labels an earlier record.

Step 1 — User intent (EV-INTENT-019-001): record the baseline statement, e.g. docs/TRUST-AND-RECOVERY.md "Backup and movement": "a successful upload is not proof of recoverability; a restore exercise is required." environment: n/a — user-intent baseline; check_date/check_method: not performed; result: intent recorded, not verified. Limitations: intent is not technical evidence.

Step 2 — Proposed design (EV-DESIGN-019-001): this workflow's template rules themselves. review_status: proposed; not accepted evidence.

Step 3 — Documentation-reviewed (EV-DOC-019-001 above): review of a draft document against criteria. Result: flag or pass on text only.

Step 4 — Component-tested (EV-COMP-019-001 template): component_identity required (upstream name plus immutable version), exact environment, result, restore_verified where backups are involved. Template values: component_identity: unresolved; environment: not performed; check_date: not performed; check_method: not performed; result: not performed; restore_verified: not performed; status: unresolved. Backup creation and restore verification are distinct records; a successful backup record is never accepted as restore verification.

Step 5 — Integration-tested (EV-INT-019-001 template): components_involved, interface_checked, fencing_behaviour where movement is covered. All values unresolved/not performed.

Progression is not automatic: evidence for the target state must exist before the state is assigned. Documentation-reviewed does not imply component-tested.

## 6. Invalidation trigger patterns (operationalized per category)

| Category | Trigger pattern | Effect | Operationalization |
|---|---|---|---|
| User intent | Baseline source file or section at pinned revision changes; coordinator reverses an intent decision. | Status → reopened; affected intent-derived records reconsidered. | Record trigger and date; re-read baseline; reopen only affected records. |
| Proposed design | Coordinator scope change; conflict with an accepted catalogue schema; baseline decision supersedes proposal. | Status → reopened or superseded. | Re-evaluate dependent documentation-reviewed records; unresolved policy stays unresolved. |
| Documentation-reviewed | Source document revision changes; acceptance criteria change; reviewer retraction; contradiction found with an accepted record. | Status → reopened; affected_records re-evaluated. | Re-run documentation review where possible; update result and limitations. |
| Component-tested | Component version, interface, environment, or procedure change; concrete failure contradicts result; restore evidence retracted. | Status → reopened; result revisited; restore_verified revisited separately. | Re-run the component check where possible; never overwrite verified-copy evidence with a failed restore. |
| Integration-tested | Either component version or interface change; fencing behaviour change; concrete failure. | Status → reopened; dependent assignment or movement records reconsidered. | Re-run integration check where possible; automatic failover evidence treated separately. |

When any trigger fires, only the affected field group or record is marked unresolved/reopened; the rest of the map is not automatically invalidated. Backup creation failure and restore verification failure are separate triggers and are recorded separately. An unresolved policy never becomes a mandate, default, or asserted test result through reopening.

## 7. Reconciliation of completed unaccepted drafts

The MAP-001 through MAP-011 drafts are examined as unaccepted reference material only. Observable points for reconciliation, none adopted as mandate:

- MAP-005's synthetic example lists `restore_verified: [synthetic]`; MAP-011 assigns `restore_verified` to component-tested restore records and keeps backup/restore distinct. Reconciled by keeping restore_verified out of catalogue-entry synthetic data and treating backup and restore as separate evidence items everywhere in this workflow.
- MAP-003 proposes `backup_policy_ref` as mandatory for assignability; MAP-004 requires the same procedure for manual and scheduled backups but names no implementation. No conflict adopted; both remain proposed.
- MAP-006 operation states (verifying, recovery-required) are status-reporting only and do not redefine the MAP-004 backup contract; this workflow preserves that boundary.

No example in this specification adopts an unresolved policy as a mandate, and no draft is treated as accepted requirements, dependency satisfaction, or verified technical evidence.

## 8. What is not claimed

- No tested capability: no component, integration, restore, or cost test has been performed.
- No upstream identity, version, licence, dependency, or cost is verified.
- No stack, provider, retention target, or recovery target is selected.
- No implementation, deployment, or external write is authorized by this task.

## 9. Acceptance criteria mapping

| MAP-019 acceptance criterion | Location |
|---|---|
| Documentation-reviewed template with all required provenance fields populated | Section 4, examples EV-DOC-019-001 and EV-DOC-019-002 |
| Invalidation trigger patterns documented for each evidence category | Section 6 |
| Five evidence categories preserved as distinct | Section 3 |
| Template records show progression path from intent to component-tested | Section 5 |
| No unsupported claims about tested capability | Section 8; all test templates marked not performed |
| Baseline intent, proposed design, unaccepted drafts, verified evidence explicitly distinguished | Sections 2 (four epistemic states) and 7 |

## 10. Proposed actions (unapproved; owners and dates unresolved)

1. Reviewer to complete documentation review of MAP-001 requirements table using the Section 4 template — owner unresolved, due unresolved.
2. Reviewer to complete documentation review of MAP-005 catalogue schema fields 4–6 — owner unresolved, due unresolved.
3. Confirm no component-tested record is created until a real component test exists — owner unresolved, due unresolved.

These actions require explicit coordinator approval before any external write.

