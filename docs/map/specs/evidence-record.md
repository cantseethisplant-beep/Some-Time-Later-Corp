# Evidence and Invalidation Records (MAP-011)

## Purpose and scope

This specification defines reusable provenance, check-result and validity records for the build map. It is the deliverable of task MAP-011 ("Define map-wide evidence and invalidation records"), prepared under claim worker hermes-laptop-map-011-auto-20261030 at repository commit 20706f1095cf9774998548660e36e2ab6be0debc, using pinned input revision 792b158838aa5214d0156690d24e21e780de542e.

Scope: provenance records, check-result records, validity conditions, invalidation triggers, synthetic examples and targeted reopening rules only. Application catalogue fields (upstream identity, licence, version, dependencies, resources, backup/restore evidence per application) remain MAP-005's responsibility and are not defined or filled in here.

Pinned inputs (user-intent baseline; no upstream technical verification):

- README.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/CONCEPT.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/DECISION-GUIDE.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e

Evidence type: user-intent baseline. No component, integration, restore or cost claim in these inputs has been technically verified.

## 1. Evidence categories (must be kept separate)

Five categories are defined. Planning text is not proof that something works, and the categories must not be collapsed:

1. User intent — what the corporation wants, taken from the pinned concept documents. Not compatibility or capacity evidence.
2. Proposed design — new schema rules proposed by MAP-011. Not accepted until separately reviewed.
3. Documentation-reviewed — a record checked against acceptance criteria by documentation review. Reviewer, date, method and result are recorded; the result concerns the document, not running software.
4. Component-tested — a measured check of one component in a stated environment. No component in this map is asserted tested; this schema exists for future accepted records.
5. Integration-tested — a measured check of two or more components together, including interfaces and fencing where movement is involved. No integration is asserted tested in this map.

Modality is preserved: "may", "should" and "must" remain distinct, and an unresolved policy never becomes a mandate through an example.

## 2. Common provenance schema (required on every record)

Required fields:

- record_id — stable identifier (for example EV-INTENT-001).
- evidence_category — one of the five categories above.
- source_file — exact repository path.
- source_revision — exact git revision of the source.
- source_section — heading or anchor used.
- environment — where the check occurred; "n/a — user-intent baseline" for intent records, "not performed" when no check exists.
- check_date — ISO-8601 date, or "not performed".
- check_method — how the result was obtained (document review, measurement, restore exercise), or "not performed".
- result — pass, flag, fail, unresolved, not performed, or "intent recorded, not verified" for intent records.
- limitations — what the result does not cover.
- invalidation_triggers — concrete changes that void the record (source revision change, component version or interface change, deployment target change, trust-assumption change, evidence change or retraction, concrete failure).
- affected_records — record IDs that must be re-evaluated when this record is invalidated or reopened.
- status — valid, superseded, reopened or unresolved.

Optional fields (include only when known; never invent): reviewer, proposal_date, review_status, measured_values, related_records, remediation, next_check_due.

Unresolved decisions stay `unresolved` with environment/check_date/check_method left as "not performed"; they are not filled with assumptions.

## 3. Category-specific additions

User-intent evidence: required fields only. environment = "n/a — user-intent baseline"; check_date/check_method = "not performed"; result = "intent recorded, not verified". Limitations must state that intent is not technical evidence.

Proposed design: adds proposed_by, proposal_date and review_status (proposed / under review / accepted / rejected). A design proposal is not evidence that the design works.

Documentation-reviewed: adds reviewer and review_method (checklist walkthrough, consistency cross-check, acceptance-criteria comparison), plus criteria_checked. Result applies to the document text.

Component-tested: adds component_identity (upstream name plus immutable version, required before any acceptance), exact environment, result, and restore_verified where backups are involved. Backup creation and restore verification are distinct records: a successful backup record is never accepted as restore verification; a restore exercise is required and is a separate component-tested record.

Integration-tested: adds components_involved, interface_checked and fencing_behaviour where movement or failover is covered.

## 4. Baseline intent versus proposed schema rules

Baseline intent (pinned inputs, not new mandates beyond what the documents say):

- CEO appoints managers and recovery custodians and approves critical policy; deployment authority and permission to decrypt backups are separate (TRUST-AND-RECOVERY).
- Managers assign only predefined approved workloads within the hardware owner's consent and limits; no arbitrary remote commands or unrestrained host access (TRUST-AND-RECOVERY).
- A backup must produce a consistent recovery package, protect it in transit and at rest, verify integrity, and record completion or failure; a successful upload is not proof of recoverability (TRUST-AND-RECOVERY).
- Planned moves verify destination consent and compatibility, quiesce writes and jobs, capture consistent state, verify the destination, change routing, fence the previous writer, and stop to a tested rollback on failure; never two authoritative writers merely because both hosts appear healthy (TRUST-AND-RECOVERY).
- The catalogue distinguishes standalone applications from add-ons and shared services (CONCEPT).
- Open questions remain: controller operator and cost, CEO identity/delegation/succession/emergency recovery, acceptable volunteer-host workloads, OS/runtime/cloud provider, spending-limit enforcement, recovery targets, owner withdrawal while offline, data-reader consent and licensing (DECISION-GUIDE).

Proposed schema rules (new from MAP-011; not accepted evidence): the five categories, the common provenance schema, invalidation_triggers and affected_records fields, and the valid / superseded / reopened / unresolved status lifecycle.

Unresolved policies (spending limits, recovery custodian succession, chosen provider, OS/runtime, RTO/RPO, licensing) are deliberately not mandated anywhere in this spec or its examples.

## 5. Synthetic examples (illustrative only — not evidence)

All examples below are synthetic. They show field usage only. No component is tested, no integration is performed, and no real upstream identity, version or licence is endorsed.

EV-INTENT-001 — user intent:

- source_file: docs/TRUST-AND-RECOVERY.md; source_revision: 792b158838aa5214d0156690d24e21e780de542e; source_section: "Backup and movement"
- environment: n/a — user-intent baseline; check_date: not performed; check_method: not performed
- result: intent recorded, not verified — a backup must produce a consistent recovery package and record completion or failure
- limitations: statement of intent; no restore evidence, no measured data-loss window
- invalidation_triggers: TRUST-AND-RECOVERY.md revision or section change
- affected_records: any component-tested or integration-tested record derived from this text
- status: valid

EV-DESIGN-001 — proposed design:

- evidence_category: proposed design; source_file: docs/map/specs/evidence-record.md; source_revision: 20706f1095cf9774998548660e36e2ab6be0debc; source_section: section 2
- proposed_by: MAP-011; proposal_date: 2026-10-30; review_status: proposed
- environment: n/a — proposal; check_date: not performed; check_method: not performed
- result: n/a — design proposal, not evidence
- limitations: not accepted; not behavioural evidence
- invalidation_triggers: coordinator scope change, conflict with MAP-005 catalogue schema
- affected_records: EV-DOC-*, EV-COMP-*, EV-INT-*
- status: proposed

EV-DOC-001 — documentation-reviewed (synthetic reviewer illustration):

- source_file: docs/TRUST-AND-RECOVERY.md; source_revision: 792b158838aa5214d0156690d24e21e780de542e; source_section: "Backup and movement"
- reviewer: synthetic reviewer (illustration only); check_date: 2026-10-30; check_method: documentation review against MAP-011 acceptance criteria
- criteria_checked: provenance fields present; backup/restore distinction preserved; no tested-component assertion
- result: flag — restore exercise required by text; no restore test exists in this map
- limitations: reviews document text only; not a restore test and not component evidence
- invalidation_triggers: TRUST-AND-RECOVERY.md revision change
- affected_records: component-tested restore records that cite this section
- status: valid

EV-COMP-001 — component-tested (synthetic; no test performed):

- component_identity: synth-backup-script v0.0.0-synthetic (illustrative; not a real upstream component)
- environment: synthetic — not a real host; check_date: not performed; check_method: not performed
- result: not performed; restore_verified: false
- limitations: synthetic example; no test executed; no restore evidence
- invalidation_triggers: component version, environment or procedure change
- affected_records: integration records that use this component
- status: unresolved

EV-INT-001 — integration-tested (synthetic; no test performed):

- components_involved: synth-backup-script v0.0.0-synthetic + synth-restore-target v0.0.0-synthetic
- interface_checked: not performed; fencing_behaviour: not performed
- environment: synthetic; check_date: not performed; check_method: not performed
- result: not performed
- limitations: synthetic example; no integration executed; no failover evidence
- invalidation_triggers: either component version or interface change
- affected_records: dependent assignment or movement records
- status: unresolved

## 6. Targeted reopening rules

Reopen only the affected record(s), never the whole map, when any of these triggers fires:

1. The source file or section at its pinned revision changes.
2. A component version, interface, deployment target or trust assumption changes.
3. Evidence the record relies on changes or is retracted.
4. A concrete failure contradicts the recorded result.
5. MAP-005 catalogue data relevant to a referenced component changes.

On reopening: set status to reopened, record trigger and date, re-run the check method where possible, update result and limitations, and re-evaluate every record listed in affected_records. An unresolved policy stays unresolved; reopening must not convert it into a mandate, a default, or an asserted test result.

## 7. Validity, reuse and limitations

A record may be reused only while its validity conditions hold: same source revision, same environment, same check method, and result not contradicted. Documentation review cannot stand in for a restore test or a measured resource test. Backup creation records are never accepted as restore verification.

Known limitations of this deliverable: the inputs are user-intent baseline only, with no upstream technical verification; no component, integration, restore or cost claim is asserted; no upstream identity, version, licence or stack is chosen; recovery-custodian rules, spending limits, recovery targets, volunteer-host workload policy and OS/runtime/provider choice remain open decisions from DECISION-GUIDE. Backup creation and restore verification remain distinct, and no restore evidence exists in this map.
