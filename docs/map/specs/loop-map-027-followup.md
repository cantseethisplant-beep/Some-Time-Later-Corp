# MAP-027 Follow-up: Backup Creation and Restore Verification Distinction Audit

**Task:** MAP-027 — Audit supplied drafts for wording that derives restore verification from backup creation
**Claim commit:** cfe54a23441982425cf5938a18f4f53c5955b493
**Worker:** hermes-laptop-map-027-auto-20261030
**Output path:** docs/map/specs/loop-map-027-followup.md
**Status:** unaccepted proposal for review only. Not accepted requirements, not technical evidence, no app implemented or tested.
**Loop:** follow-up, cycle 3, area recovery, key gap-key-backup-restore-distinction, loop policy 1.

## 1. Purpose, scope, and evidence status

This file is the deliverable of task MAP-027. It audits the supplied drafts for any wording that derives restore verification from backup creation or upload success, and confirms that each draft keeps backup creation and restore verification as distinct evidence items with `restore_verified` never derived from a backup record.

**Evidence status.** The four pinned baseline inputs (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md at revision 792b1588...) are user-intent baseline only; no upstream technical verification exists. Every checked draft listed in the task contract is an UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY: not requirements, not dependency satisfaction, not technical evidence. Nothing in this audit upgrades any draft to accepted status, and no backup test, restore test, or runtime check is claimed.

**Audit rule.** For each checked draft and section: identify backup-creation fields/outcomes and restore-verification fields/outcomes; confirm they are separate record concepts; confirm `restore_verified` (or its equivalent) is never derived from a backup record, successful upload, or integrity check. Modality ("may"/"should"/"must") is preserved; no unresolved policy is upgraded into a mandate. Where residual phrasing conflates the two, a minimal correction traceable to the draft and section is drafted. Where none is found, the outcome is recorded as "confirmed: no change required" with the checked sections cited as provenance.

## 2. Classification boundaries

- **Baseline intent:** the four concept documents at 792b1588.... They state that a successful upload is not proof of recoverability and that a restore exercise is required. Intent is not evidence.
- **Proposed design:** field lists, outcome labels, record shapes, and validation rules added by MAP-004/MAP-005/MAP-011 and by this audit's drafting; pending separate acceptance.
- **Completed unaccepted reference drafts:** MAP-001 through MAP-015 and MAP-017/MAP-019/MAP-023 follow-ups, reviewed here only to find contradictions or conflation. They are not accepted.
- **Genuinely verified evidence:** none exists in this map. No backup or restore test has been performed.

## 3. Checked drafts, sections, and separation results

| Draft | Revision | Path | Sections checked | Backup creation item | Restore verification item | Separation result |
|---|---|---|---|---|---|---|
| MAP-004 Backup and Recovery Outcomes | ccf0957af... | docs/map/specs/backup-recovery.md | §2, §5, §6 | Operation labels Requested/Running/Verified copy/Failed; retained-copy record; backup operation record | Restore-tested result category (attempted/succeeded/failed/not performed); restore exercise record; custodian | Separate. §2: "Restore-tested is not a copy lifecycle state." §5: "A successful upload or integrity check does not prove recoverability." §6: failed restore does not overwrite verified-copy evidence. |
| MAP-005 Catalogue Entry and Evidence Fields | 96464d4... | docs/map/specs/catalogue-entry.md | §4.6, §7, §9 | backup_schedule, backup_consistency, backup_integrity, backup_keys_managed_separately, backup_record | restore_exercise, restore_verified (boolean), acceptable_data_loss_window | Separate. §9: "`restore_verified` is never derived from a backup upload." Synthetic example lists both as independent `[synthetic]` placeholders. |
| MAP-011 Evidence and Invalidation Records | 119bb89... | docs/map/specs/evidence-record.md | §3, §7 | Backup creation record | `restore_verified` on component-tested restore records; restore exercise required as separate record | Separate. §3: "a successful backup record is never accepted as restore verification." §7: "Backup creation records are never accepted as restore verification." |
| MAP-019 Evidence Categorization and Validation Workflow | 41c48fe... | docs/map/specs/loop-map-019-followup.md | §3, §5, §7 | Backup record as an evidence item | Restore verification as a separate evidence item; `restore_verified: not performed` in component-tested template | Separate. §3: "Backup creation and restore verification are distinct evidence items..." §7 reconciles MAP-005/MAP-011 by keeping both separate everywhere. |
| MAP-023 Node Approval and Restore-Proof Reconciliation | 810cc1f... | docs/map/specs/loop-map-023-followup.md | §5, §6 | Backup integrity (consistent package, protected, integrity verified) | Restore verification (restore exercise result; attempted/succeeded/failed/not performed) | Separate. §4 proposed wording: "One does not imply the other." §5 crosswalk retains upload≠recoverability and leaves restore-gating unresolved. |

Total: 13 section checks across 5 drafts.

## 4. Section-by-section findings

**MAP-004 §2 (Outcome labels by record concept).** Backup operations carry labels Requested, Running, Verified copy, Failed. Restore-tested is defined as a restore-exercise result category, not a copy lifecycle state, with sub-states attempted, succeeded, failed, not performed. A Verified copy enters Restore-tested only at the restore-exercise record level, and a failed restore does not overwrite the copy's Verified copy evidence. The repository claims no restore test. Finding: separate; no conflation.

**MAP-004 §5 (Evidence a later restore task must supply).** The restore-exercise evidence list (source revision, procedure version, verified copy used, target, steps, observed result, custodian) is distinct from backup operation evidence. It states that a successful upload or integrity check does not prove recoverability, and that the evidence list is not evidence that any restore has been performed. Finding: separate; no conflation.

**MAP-004 §6 (Proposed record concepts).** Backup operation record, retained-copy record, and restore exercise record are separate shapes. Validation rule: "a failed restore does not overwrite existing verified-copy evidence"; Restore-tested is recorded only after an exercise result exists. Finding: separate; no conflation.

**MAP-005 §4.6 (Backup and restore evidence — distinct items).** Fields are grouped as backup fields (backup_schedule, backup_consistency, backup_integrity, backup_keys_managed_separately, backup_record) and restore fields (restore_exercise, restore_verified, acceptable_data_loss_window). `restore_verified` is a boolean with the note: "A successful upload is not proof of recoverability; only a restore exercise counts." Finding: separate; no conflation.

**MAP-005 §7 (Synthetic unverified example).** The example block lists `backup_record: none [synthetic]`, `restore_exercise: none [synthetic]`, and `restore_verified: [synthetic]` as independent placeholders. No value derives one from the other; all are marked synthetic. Finding: separate; no conflation.

**MAP-005 §9 (Acceptance checks).** Explicit check: "Backup fields and restore fields are separate; `restore_verified` is never derived from a backup upload." Finding: separate; this section is itself a provenance citation for the distinction.

**MAP-011 §3 (Category-specific additions).** Component-tested records add `restore_verified` where backups are involved, and state: "Backup creation and restore verification are distinct records: a successful backup record is never accepted as restore verification; a restore exercise is required and is a separate component-tested record." Finding: separate; no conflation.

**MAP-011 §7 (Validity, reuse and limitations).** States: "Backup creation records are never accepted as restore verification." Finding: separate; no conflation.

**MAP-019 §3 (Five evidence categories).** States: "Backup creation and restore verification are distinct evidence items; a successful backup record is never accepted as restore verification." Categories must never be merged into a single flag. Finding: separate; no conflation.

**MAP-019 §5 (Progression path).** Step 4 component-tested template sets `restore_verified: not performed` and repeats that a successful backup record is never accepted as restore verification. Finding: separate; no conflation.

**MAP-019 §7 (Reconciliation of completed unaccepted drafts).** Reconciles MAP-005's synthetic `restore_verified: [synthetic]` with MAP-011's component-tested `restore_verified` by keeping `restore_verified` out of catalogue synthetic data and treating backup and restore as separate evidence items everywhere in the workflow. Finding: separate; no conflation.

**MAP-023 §5 (Source/modality crosswalk) and §6 (Distinctions preserved).** §5 crosswalk retains "restore exercise required to prove recoverability" intact and "successful upload is not proof of recoverability"; restore-before-approval is relabelled proposed design, not baseline-mandated; results include "not performed." §6 states: "a Verified copy (integrity checked, stored at rest) is not a restore-tested copy; restore-exercise evidence is a separate record concept." The proposed replacement wording in §4 adds: "Backup integrity ... is distinct from restore verification ... One does not imply the other." Finding: separate; no conflation.

## 5. Audit finding

**Outcome: confirmed — no change required.**

No supplied draft in the checked sections derives `restore_verified` (or restore verification generally) from backup creation, backup upload success, or integrity-check success. Every checked section keeps backup creation and restore verification as distinct evidence items, and every draft preserves the baseline rule that a successful upload is not proof of recoverability.

Because no residual conflation was found, no minimal correction draft is produced. If a later review finds conflation, any correction must cite the specific draft, revision, path, and section, and must be proposed design only (not baseline intent and not verified evidence).

**Provenance list (checked sections):** MAP-004 §2, §5, §6; MAP-005 §4.6, §7, §9; MAP-011 §3, §7; MAP-019 §3, §5, §7; MAP-023 §5, §6 (with supporting proposed wording in MAP-023 §4).

## 6. Limitations

- No GitHub, terminal, network, or delegation tools are available; board state and file SHAs were not independently verified.
- All checked drafts are unaccepted completed drafts for review only; this audit is review input, not acceptance.
- Evidence type is user-intent baseline only; no upstream technical verification exists for any backup or restore behaviour.
- No backup, restore, component, or integration test was performed, and none is claimed.
- Modality was preserved; no unresolved policy was converted into a mandate in examples.

## 7. Acceptance criteria mapping

1. Cited list of checked drafts and sections showing backup fields and restore fields are separate: Section 3 table and Section 4 findings (including MAP-005 §9 and MAP-023 §6 as examples).
2. Recorded finding that no supplied draft derives `restore_verified` from backup upload: Section 5 ("confirmed: no change required") with the provenance list of checked sections. No correction draft was required because no conflation was found.
3. Baseline intent, proposed design, completed unaccepted reference drafts, and genuinely verified evidence are explicitly distinguished: Sections 1 and 2; verified evidence is empty.

## 8. Review pending

Yes. This draft is review input only. Acceptance rests with the project owner or an appointed reviewer; nothing is self-accepted.

