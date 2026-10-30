# Operation status and failure reporting

## 1. Purpose and scope

This specification defines user-visible operation states and truthful progress and error reporting for the Eve Cloud hosting-manager concept. It covers the lifecycle of an operation such as deploying an application assignment, taking a scheduled or on-demand backup, moving an assignment between hosts, or performing an authorised recovery exercise. It deliberately does not choose a transport protocol, scheduling implementation, database schema, worker queue, retry algorithm, or API surface. Those are implementation decisions for later tasks.

This task takes only the repository inputs named in claim MAP-006: README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md and docs/TRUST-AND-RECOVERY.md, all at revision 792b158838aa5214d0156690d24e21e780de542e. No external research was performed and no component tests exist. Every statement below traces to those inputs or is explicitly marked as unresolved policy.

The acceptance criteria require coverage of requested, authorised, queued, running, verifying, completed, failed, cancelled and recovery-required distinctions; timeout and unknown outcome handling; retry and idempotency requirements; synthetic worked cases; undecided policy flags; and an explicit boundary so that this specification does not redefine the backup-specific contract owned by MAP-004.

## 2. Baseline intent from inputs

The concept documents describe intended behaviour, not available features. Relevant baseline statements include:

- A manager proposes an assignment within the hardware owner's consent and limits; the platform prepares and verifies a controlled deployment on an approved host.
- Authorised users monitor health, request backups, or use scheduled backups.
- If hosting changes, the platform follows an application-specific movement or recovery procedure, recording what succeeded and what needs attention.
- A backup button and a timed backup should use the same verified procedure.
- A successful upload is not proof of recoverability; a restore exercise is required.
- For a planned move: verify destination consent and compatibility; prepare the reviewed version; quiesce writes and jobs; capture or hand over consistent state; verify the destination; change routing; fence the previous writer before admitting new writes; if verification fails, stop and use a tested rollback procedure; never allow two authoritative writers merely because both hosts appear healthy.
- Existing workloads should keep running during controller outages, subject to their own dependencies; this must be tested.
- Automatic failover is a later capability requiring its own evidence.

None of these statements defines specific operation statuses, progress fields, retry rules, or idempotency keys. Those rules are proposed in this specification as the MAP-006 deliverable and remain unverified until accepted.

## 3. Operation state model

Every tracked operation has exactly one lifecycle state at a time. States are user-visible and may be exposed in dashboards, notifications, and recovery records. Transitions between states are constrained: an operation may not move directly from running to completed without a verifying step, and an operation may not move from failed back to running without an explicit retry or re-authorisation decision.

### 3.1 Defined states

| State | Meaning | Terminal? | May be retried? | Cancellable? |
|-------|---------|-----------|-----------------|--------------|
| requested | A user or scheduler has submitted an operation and it has not yet been authorised. | No | N/A | Yes |
| authorised | An authorised actor has approved the operation; scheduling has not yet placed it on a queue. | No | N/A | Yes |
| queued | The operation is waiting for a worker, host, or scheduling window. | No | No | Yes |
| running | The operation is actively executing on a host. | No | No direct retry; failed runs may be retried per policy | Yes |
| verifying | The operation has finished its primary work and is checking the result against acceptance conditions. | No | Verification failure moves to failed | Yes |
| completed | The operation succeeded and its result was verified where applicable. | Yes | N/A | No |
| failed | The operation did not complete successfully; a reason is recorded. | Yes | Yes, per retry and idempotency rules | No |
| cancelled | The operation was stopped before completion by user action, host revocation, or scheduling policy. | Yes | N/A | No |
| recovery-required | The operation completed but with conditions requiring recovery attention, or a dependent operation failed and left partial state. | No | No automatic retry; recovery custodian review required | No |

The distinction between completed and failed must never be inferred from launch alone. Launching a deployment, backup upload, or move does not constitute success. Completed requires evidence appropriate to the operation type; for backup and recovery operations this aligns with the TRUST-AND-RECOVERY.md principle that a successful upload is not proof of recoverability and that a restore exercise is required.

The recovery-required state is distinct from failed. A failed operation did not complete its primary work. A recovery-required operation may have completed its primary work but leaves the system in a state that needs human or custodian action, such as an unverified restore, a move where fencing of the previous writer is incomplete, or an assignment whose host consent was withdrawn mid-operation.

Cancellation and retry are separate transitions. Cancellation stops an operation before completion; retry applies only to failed operations per section 5.1. Whether running or verifying operations can be cancelled, and under what conditions, is proposed by this specification and not defined by the inputs.

### 3.2 States not created by this specification

This specification does not define host-level states such as online, offline, draining, or maintenance, nor assignment lifecycle states such as active, expired, or withdrawn. Those belong to host-management and assignment tasks. It also does not define the MAP-004 backup-specific contract, including backup retention, encryption key separation, integrity verification details, or restore-procedure evidence. References to backup and recovery here are limited to status reporting for operations that involve backup, movement, or recovery as workloads.

## 4. Truthful progress and error reporting

Every operation record must carry enough information for a user to understand what happened without inferring success from activity.

### 4.1 Minimum record fields

- operation identifier
- operation type (for example deploy, backup, move, recovery)
- current lifecycle state
- owner or requesting actor
- target host or assignment reference
- started-at timestamp
- last-updated timestamp
- finished-at timestamp, present only when the state is terminal (completed, failed, or cancelled)
- current step or stage, if the operation type defines stages
- progress numerator and denominator, or an explicit "unknown" marker when progress cannot be measured
- outcome summary for terminal states
- failure reason or error class for failed and recovery-required states
- retry count and retry eligibility
- idempotency key, if the operation supports retries
- citations to the operation log or step record where available

Progress must not be fabricated. If the platform cannot measure how much work remains, the record must state "unknown" rather than inventing a percentage or time estimate. A timestamp is not a status: last-updated changing does not imply the operation is healthy, and silence must not be read as progress.

### 4.2 Timeout and unknown outcome

Operations must support a configured timeout per operation type. When an operation exceeds its timeout without reaching a terminal state, its state must transition to failed with an explicit timeout reason, or to recovery-required if partial state may exist and safe automatic failure determination is not possible. The record must mark the outcome as unknown until evidence resolves it.

An unknown outcome is not a failure, and not a success. It must be displayed to users as "outcome unknown" and must not trigger downstream actions that assume either completed or failed. For example, a move operation whose destination verification times out must not be treated as moved until verification resolves; the previous writer must remain fenced or isolated until the outcome is known.

### 4.3 Error classes

Failures must be reported with an error class so users and recovery procedures can distinguish transient from permanent conditions:

- transient: network blip, host temporarily unreachable, queue backlog. Eligible for retry.
- permanent: invalid assignment, missing reviewed version, host consent withdrawn, unsupported application. Not eligible for retry without user intervention.
- resource: insufficient CPU, memory, storage, or licence seats. Retry only after the resource constraint is addressed.
- timeout: operation exceeded its configured deadline. Outcome unknown until resolved.
- partial-state: operation completed some work but cannot confirm the final result. May require recovery-required.

Error class is a proposal in this specification; the mapping from specific platform errors to these classes is not defined by the inputs and remains open.

## 5. Retry and idempotency requirements

### 5.1 Retry eligibility

Only failed operations with a transient error class and remaining retry budget may be retried automatically. Permanent errors require explicit user or manager action before a new operation is requested. Timeout errors create an unknown outcome and must not be auto-retried until the outcome is resolved, because retrying an operation whose primary effects may have already occurred risks duplicate writers or double billing.

The number of retry attempts, backoff timing, and which transient errors qualify are policy decisions not present in the inputs. They are marked unresolved below.

### 5.2 Idempotency

Any operation that may be retried must support an idempotency key supplied by the caller or generated by the platform at request time. Retrying with the same key must not produce duplicate authoritative effects. For move operations, this is critical: the TRUST-AND-RECOVERY.md baseline explicitly forbids allowing two authoritative writers merely because both hosts appear healthy.

Idempotency does not mean "safe to repeat forever." It means the platform can recognise a repeat of the same logical operation and avoid duplicating effects that have already occurred. Whether idempotency keys are caller-supplied, platform-generated, or both is unresolved.

### 5.3 Never infer success from launch

This is a hard requirement repeated from the acceptance criteria. Submitting, authorising, queueing, or starting an operation is not evidence that it succeeded. Completed status requires verified evidence appropriate to the operation type. For deployment and movement, verification is part of the lifecycle (the verifying state). For backup and recovery, recovery procedures and restore evidence are governed by MAP-004 and the trust-and-recovery inputs, not by this status model alone.

## 6. Synthetic cases

The following cases illustrate how the state model applies. They are synthetic examples, not requirements, and any policy choices they depend on are flagged as undecided.

### 6.1 Deployment on a trusted host

A manager requests deployment of a reviewed application bundle to a volunteered host within the owner's limits.

1. requested: manager submits the deployment.
2. authorised: CEO or appointed manager approves within the host owner's consent.
3. queued: deployment waits for the host's next operating window.
4. running: platform prepares and starts the reviewed version on the approved host.
5. verifying: platform checks the deployment against the application-specific acceptance conditions.
6. completed: verification passes; the record notes what was verified.

Undecided: what acceptance conditions constitute a verified deployment for each application type. This is application-specific and outside MAP-006 scope.

### 6.2 Scheduled backup

A timed backup runs according to a schedule. The backup-specific contract is owned by MAP-004; this case covers status reporting only.

1. requested or queued: the schedule triggers the backup operation.
2. running: the backup procedure runs on the approved host.
3. verifying: the operation record notes that a verification step under the MAP-004 contract was invoked; mechanics and pass/fail criteria are owned by MAP-004 and deferred here.
4. completed: the record states that the MAP-004 verification outcome passed, not merely that the upload finished.
5. failed: if verification under the MAP-004 contract does not pass, or the host is offline, the state is failed with reason; a successful upload alone does not produce completed.

Undecided: retry scheduling for failed backups, and whether a failed scheduled backup retries on the next schedule or requires manager intervention. Integrity-check details are deferred to MAP-004.

### 6.3 Planned move between hosts

1. requested: move proposed to destination host.
2. authorised: destination consent and compatibility verified.
3. queued: move awaits the movement window.
4. running: writes and jobs quiesced; consistent state captured or handed over.
5. verifying: destination verified; previous writer fenced before new writes admitted.
6. completed: routing changed and previous writer fenced.
7. failed: if verification fails at any point, the move stops and a tested rollback procedure is used; two authoritative writers are never allowed merely because both hosts appear healthy.

Undecided: rollback procedure details and fencing mechanism are application-specific.

### 6.4 Timeout with unknown outcome

A deployment to a member host loses network contact during running. The operation exceeds its configured timeout.

- State transitions to failed or recovery-required with reason "timeout".
- Outcome is marked unknown.
- No automatic retry until the outcome is resolved, because the deployment may have partially completed on the host.
- A hardware owner or recovery custodian inspects the host before any further operation on that assignment.

Undecided: the default timeout value per operation type and who resolves an unknown outcome.

### 6.5 Recovery-required after partial move

A move reaches verifying, the destination is verified, but fencing of the previous writer cannot be confirmed before the recovery custodian's shift ends.

- State becomes recovery-required, not completed and not failed.
- The record notes what succeeded (destination verified) and what needs attention (previous-writer fencing).
- No new writes are admitted to either host until the custodian resolves fencing.

Undecided: who may resolve recovery-required states and within what SLA.

## 7. Undecided policy

The following policy items are intentionally not decided by this specification. They must not be treated as mandates in examples or implementation work:

- Default timeout values per operation type.
- Maximum retry count and backoff schedule per error class.
- Which transient error classes are auto-retried versus requiring manager approval.
- Whether idempotency keys are caller-supplied, platform-generated, or both.
- The SLA or owner for resolving recovery-required states.
- Whether a failed scheduled backup retries automatically on the next schedule.
- Application-specific deployment acceptance conditions and rollback procedures.
- Host-level states and assignment lifecycle states.

These items are marked unresolved because the inputs do not contain them. An implementation that adopts values for them is making new policy decisions beyond MAP-006.

## 8. Boundaries and exclusions

- MAP-004 owns the backup-specific contract: retention, encryption and key separation, integrity verification, restore-procedure evidence, and the distinction between backup and live standby. This specification references backup only as an operation type with status reporting.
- Automatic failover is a later capability requiring its own evidence; this specification does not define failover states or triggers.
- Cloud networking, storage, scheduling, and application hosting are separate responsibilities. This specification does not choose a cloud provider or scheduling mechanism.
- Deployment authority and permission to decrypt backups should remain separate per TRUST-AND-RECOVERY.md; this specification does not define access-control rules for viewing or transitioning operation states.

## 9. Open questions for the next task

1. Which operation types are in the pilot scope: deploy, backup, move, recovery, or a subset?
2. What are the default timeouts and retry budgets per operation type?
3. Who resolves recovery-required states, and what is the expected response time?
4. How do operation states surface to hardware owners without exposing host OS or personal file details?
5. What audit log format records state transitions for recovery custodians and CEO review?

These questions are listed for discovery; they are not permission to expand build scope automatically.

## 10. Acceptance checklist

- [ ] Requested, authorised, queued, running, verifying, completed, failed, cancelled, and recovery-required states are defined and distinguished.
- [ ] Timeout and unknown outcome handling is specified without inferring success from launch.
- [ ] Retry eligibility and idempotency requirements are specified with unresolved policy clearly flagged.
- [ ] Backup-specific contract is not redefined; MAP-004 boundary is stated.
- [ ] Synthetic cases are included with undecided policy flagged.
- [ ] No transport, implementation, runtime test, or external dependency is assumed.
