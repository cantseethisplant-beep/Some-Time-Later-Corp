# Backup and Recovery Outcomes (MAP-004)

**Task:** MAP-004 — Specify backup and recovery outcomes
**Commit:** a26a5e02f50815a1d94e39f76d6880b269aa7874
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e
**Inputs:** README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md
**Output path:** docs/map/specs/backup-recovery.md
**Status:** proposed specification, not accepted work. This repository is concept and planning only; there is no working app, supported deployment, or measured restore (README.md). No completed restore test is claimed by this file.

## 1. Purpose, scope, and evidence status

This specification defines the outcomes that manual and scheduled backup and recovery operations must reach. It does not choose a storage vendor, transfer mechanism, or encryption implementation.

**Baseline intent (user-approved inputs).** The four pinned inputs express product intent: both a backup button and timed backups are expected; a backup must produce a consistent recovery package, protect it in transit and at rest, verify integrity, and record completion or failure; a successful upload is not proof of recoverability, and a restore exercise is required; deployment authority and permission to decrypt backups should be separate; keys must be managed separately from encrypted copies; a backup is not a live standby, and an offline host cannot make a new backup. Planned move and emergency recovery behaviour is described in docs/TRUST-AND-RECOVERY.md.

**Proposed design (new, not settled baseline).** The outcome labels, record shapes, validation rules, and worked examples below are proposed design produced for this task. They are implementation-guidance candidates, not verbatim requirements from the inputs. No example adopts an unresolved policy as a mandate.

Scope covers the backup copy lifecycle, consistency requirements for planned moves, roles around recovery access, the evidence a later restore task must supply, and the values intentionally left unresolved. Out of scope: storage provider selection, encryption algorithms, key-management implementation, cloud cost controls, automatic failover, and any Discord integration.

## 2. Outcome labels by record concept

Every record carries an outcome label appropriate to its record type. Operation state, retained-copy verification state, and restore-exercise result are separate record concepts (Section 6) and must not be collapsed into a single flag or shared label vocabulary.

**Operation labels** apply to backup operations: Requested, Running, Verified copy, Failed.

- **Requested**: a backup was asked for — by a user clicking the backup button or by a scheduled timer — but copy work has not begun. Entry: request accepted, target application and host identified. Exit: copy work starts (Running) or the request is rejected or aborted (Failed). Evidence: request source (manual or scheduled), target, requested time. Modality: required; the concept expects both a backup button and timed backups (docs/CONCEPT.md).
- **Running**: copy work is in progress: data is being read, packaged, protected in transit, and written to the destination. Entry: request accepted and copy work started. Exit: integrity verified and copy stored at rest (Verified copy), or any step fails (Failed). Evidence: start time, target, host identity, procedure version in use. Modality: required; completion or failure must be recorded (docs/TRUST-AND-RECOVERY.md).
- **Verified copy**: a consistent recovery package exists at rest, its integrity has been verified, and completion has been recorded. Entry: Running ends with a successful integrity check and durable storage at rest. Exit: retention action, selection for a restore exercise, or supersession. Evidence: integrity check result, storage location, completion time, retention class. Modality: required; a backup must produce a consistent recovery package, protect it in transit and at rest, verify integrity, and record completion or failure (docs/TRUST-AND-RECOVERY.md).
- **Failed**: any part of copying failed before a verified copy existed: rejected request, read error, transit error, storage error, integrity failure, or host unavailable. Entry: Running terminates unsuccessfully or a request cannot start. Exit: new request (Requested) or incident closed without retry. Evidence: failure step, error class, time, target, whether any partial copy exists. Modality: required; failures are recorded as failures, never silently recast as success.

**Retained-copy status**: a retained copy is a Verified copy carrying retention status (retained, superseded, removed). Retention action, supersession by a newer copy, or removal changes status; it does not change the operation outcome.

**Restore-tested** is not a copy lifecycle state. It is a restore-exercise result category, with sub-states attempted, succeeded, failed, not performed. A Verified copy selected for a restore exercise enters Restore-tested only at the restore-exercise record level; the copy's Verified copy evidence is not overwritten by a failed restore (Sections 5–6). This repository claims no restore test.

## 3. Behaviour rules

1. Same procedure for manual and scheduled backups. A backup button and a timed backup must use the same verified procedure (docs/CONCEPT.md).
2. Consistent capture for routine backups. Routine manual and scheduled backups require an application-specific consistent capture procedure plus integrity and protection evidence (in transit and at rest). Quiescing may be adapter-specific rather than universal and is not a universal requirement to stop services. Completion or failure is recorded (docs/TRUST-AND-RECOVERY.md).
3. No live standby. A backup is not a live standby. An offline host cannot make a new backup, and recovery may lose changes since the most recent usable copy (docs/TRUST-AND-RECOVERY.md; docs/DECISION-GUIDE.md).
4. No vendor or encryption choice. Storage provider and encryption implementation are unspecified. Key separation is required by baseline — keys must be managed separately from encrypted copies — but the implementation is unresolved (docs/TRUST-AND-RECOVERY.md).
5. Planned move or cutover (separate scenario). Verify destination consent and compatibility; prepare the reviewed version; quiesce writes and jobs; capture or hand over consistent state; verify the destination; change routing; fence the previous writer before admitting new writes; if verification fails, stop and use a tested rollback procedure. Never allow two authoritative writers merely because both hosts appear healthy (docs/TRUST-AND-RECOVERY.md). These steps apply to planned moves, not to routine backups.
6. Emergency recovery. Requires a prepared target and accessible recovery data. Automatic failover is a later capability requiring its own evidence (docs/TRUST-AND-RECOVERY.md).
7. Controller resilience. The controller needs reliable storage and hosting of its own; workloads should keep running during controller outages subject to their own dependencies, and this must be tested (docs/CONCEPT.md).

## 4. Roles and unresolved values

Roles come from the baseline: the CEO appoints managers and recovery custodians; a recovery custodian retrieves or restores specifically authorised recovery material; deployment authority and permission to decrypt backups are separate; CEO succession must not silently grant access to every historical secret (README.md; docs/TRUST-AND-RECOVERY.md).

The following values are intentionally unresolved. None is a mandate, default, or permission to implement:

- Custodian access: who may be recovery custodian, which recovery material may be retrieved or restored, and under what authorisation. Exact rules remain a design decision.
- Key separation implementation: how keys are stored, rotated, and separated from encrypted copies. No key management system or algorithm is selected.
- Offline hosts: behaviour when an assigned host is offline (missed scheduled backup, no new backup, recovery from the most recent usable copy) and how hardware owners are notified. Withdrawal of an offline host is an open question (docs/DECISION-GUIDE.md).
- Retention: how long verified copies are kept, how many copies per target, rotation, and deletion. Unresolved.
- Acceptable data-loss and recovery targets: recovery time and data-loss targets per application are open questions (docs/DECISION-GUIDE.md). They must be decided per application before a restore task can judge whether a copy is acceptable.

Illustrative baseline settings — a trusted host running an authentication bundle, a Sunday maintenance window, backups every six hours, recovery access for the CEO and an appointed officer — are explicitly illustrative, not universal defaults (docs/CONCEPT.md). They are not adopted by this specification.

## 5. Evidence a later restore task must supply

A later task performing or verifying a restore must supply, for each restore exercise:

- the source input revision and the restore procedure version used;
- the Verified copy used, with its integrity evidence and completion time;
- the restore target, and destination consent/compatibility evidence where a move is involved;
- the steps performed. For an isolated restore exercise: no disruption of live routing or writers; for a production migration/cutover: quiesce, capture or handover, verification, routing change, fencing of the previous writer, rollback trigger if used;
- the observed result: successful or unsuccessful, including data loss since the most recent usable copy and time to recover;
- confirmation that no two authoritative writers were admitted simultaneously (applies to cutover, not to an isolated restore exercise);
- the custodian who authorised or performed the restore.

Restore-exercise results are separated: attempted, succeeded, failed, not performed. A successful upload or integrity check does not prove recoverability; a failed restore leaves a visible failure and no success certification. This specification claims no completed restore tests; this evidence list is not evidence that any restore has been performed.

## 6. Proposed record concepts

These record shapes and validation rules are proposed design for this task, not verbatim settled baseline requirements.

**Backup operation record:** operation id, source (manual or scheduled), target application and host, requested time, outcome (Requested/Running/Verified copy/Failed), failure step and error class if failed, partial-copy flag, procedure version, retention class.

**Retained-copy record:** copy id, storage location, integrity check result, completion time, retention class, superseded-by copy id, removed-at time.

**Restore exercise record:** exercise id, source copy id, result (attempted/succeeded/failed/not performed), result evidence, data loss since most recent usable copy, time to recover, custodian, live routing or writers affected (must be false for an isolated exercise).

**Validation rules:** a rejected request ends as Failed, never success; a retry is a new operation; a failed restore does not overwrite existing verified-copy evidence; retention removal removes the retained copy but not operation history; Restore-tested is recorded only after an exercise result exists.

## 7. Worked examples (synthetic)

**Example A — successful copy, then failed restore exercise (abbreviated).**

1. Scheduled backup for an application on host H: operation O1 enters Requested at request time t1, then Running; the integrity check passes and the copy is stored at rest as copy C1 (Verified copy) at completion time t2. Evidence: integrity check result, storage location, t2, retention class.
2. Restore exercise E1 selects C1: its result is recorded as failed, with failure step and error class; no success certification is issued; evidence for C1 remains intact and C1 remains a Verified copy unless retention later supersedes it.

Abbreviation note: O1 and C1 omit Section 6 fields not needed for this flow (partial-copy flag, procedure version, superseded-by, removed-at); E1 omits custodian, data loss since most recent usable copy, time to recover, and result evidence, all marked pending for this synthetic case; live routing/writers affected is explicitly false because this is an isolated exercise, not a cutover (Section 5; Section 6).

Check: the same procedure would apply to a manual backup; no vendor, timing, provider, or numerical default is invented; a failed restore is not recast as success (Section 2; Section 6).

**Example B — planned move condition.**

For application A moving from host H1 to host H2: destination consent and compatibility verified; reviewed version prepared; writes and jobs quiesced; consistent state captured or handed over; H2 verified; routing changed; previous writer on H1 fenced before new writes; if H2 verification fails, stop and use tested rollback; never two authoritative writers. This cutover is distinct from a backup, and an isolated restore exercise must not instruct disruption of live routing or writers.

Check: all steps come from docs/TRUST-AND-RECOVERY.md; no timing, provider, or cost values are assumed; no unresolved policy (custodian access, key separation, retention, targets) is treated as a mandate (Section 4).

## 8. Limitations

- Derived solely from the four concept and planning documents at input revision 792b158838aa5214d0156690d24e21e780de542e; evidence type is "user-intent baseline; no upstream technical verification."
- No upstream software identity, version, licence, dependency, or cost has been verified; no storage vendor or encryption implementation is chosen.
- This worker performed no backup or restore test and claims none; nothing here asserts the absence of evidence outside the supplied inputs.
- This is a specification of outcomes, not production implementation guidance; unresolved values require decisions before implementation.

## 9. Acceptance criteria mapping

| Task acceptance criterion | Location in this specification |
| --- | --- |
| Separate requested, running, verified copy, failed and restore-tested outcomes | Section 2 |
| Custodian access, key separation, offline hosts, retention questions, acceptable data-loss/recovery targets as unresolved values | Section 4 |
| Evidence a later restore task must supply; no completed restore tests claimed | Section 5 |
