# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/8

Automated critic only; independent review pending.

# MAP-006 finished-work handoff

## Task and claim
- Task ID: MAP-006
- Claim commit: 6f829ebc6495e525b5365d348190e61fe563dd61
- Claim token: zxzrthNOKK6AdaKuutgp_np92e-uMkl1
- Worker ID: hermes-laptop-map-006-auto-20261030
- Branch: hermes/map-006-auto-20261030
- Input revision: 792b158838aa5214d0156690d24e21e780de542e
- Run: eve-blueprint-20261030
- Output path: docs/map/specs/operations.md

## Exact sources
- README.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/CONCEPT.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/DECISION-GUIDE.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e

## Diagnosed issues and exact corrections
1. Section 3.1 table, row 'queued', column 'May be retried?': previous value 'Yes, cancellation permitted' conflated cancellation with retry. Correction: added a separate 'Cancellable?' column; the queued row now reads 'No' for retry and 'Yes' for cancellable. Retry applies only to failed operations per section 5.1; cancellation is a separate terminal transition.
2. Section 6.2 'Scheduled backup': previous text asserted backup integrity-verification mechanics that section 8 assigns to MAP-004. Correction: rephrased the verifying step to note that a verification step under the MAP-004 contract was invoked, with mechanics and pass/fail criteria owned by MAP-004 and deferred here; completed requires the record to state the MAP-004 verification outcome passed, not merely that the upload finished; integrity-check details explicitly deferred to MAP-004.
3. Section 4.1 minimum field 'completed-at timestamp': correction — renamed to 'finished-at timestamp', present only when the state is terminal (completed, failed, or cancelled), so the name is not semantically wrong for failed and cancelled states.
4. Section 6.1: correction — changed 'deployment of an reviewed application bundle' to 'a reviewed application bundle'.

## Remaining uncertainty
- All section 7 undecided policy items remain unresolved: default timeouts, retry counts and backoff, auto-retry eligibility, idempotency key ownership, recovery-required SLA/owner, scheduled-backup retry behaviour, application-specific acceptance conditions and rollback procedures, and host/assignment lifecycle states.
- Whether running or verifying operations can be cancelled, and under what conditions, is proposed by this specification and not defined by the inputs.
- No transport, scheduling, database, retry algorithm, or API surface is chosen.

## Checks actually performed
- Compared all nine required states (requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required) against section 3.1 and the acceptance checklist in section 10.
- Verified section 4.2 timeout/unknown outcome handling and synthetic case 6.4 do not infer success from launch and mark outcome as unknown until evidence resolves.
- Verified section 5.1 limits automatic retry to failed operations with transient error class and remaining retry budget; section 5.2 requires an idempotency key for retriable operations.
- Checked synthetic cases 6.1–6.5 against required fields and flagged undecided policy in each case.
- Verified the MAP-004 boundary is stated in sections 6.2, 8 and 10; the backup-specific contract (retention, encryption and key separation, integrity verification details, restore-procedure evidence) is not redefined.
- Confirmed unresolved policy items in section 7 are not restated as mandates in the synthetic examples.

## Limitations
- No GitHub, terminal, network or delegation tools are available; the live board could not be fetched, inputs could not be independently verified, and no tests could be run.
- Evidence type is user-intent baseline only; no component tests or runtime tests exist.
- No implementation stack, cloud provider, or external dependency is assumed or selected.

## Remaining work
- Coordinator or project owner review of the draft against MAP-006 acceptance criteria.
- Resolution of section 7 undecided policy items in later map tasks.
- Integration with MAP-004 backup contract and other map tasks as they are accepted.

## Review pending
- Yes. This draft is submitted for review; no acceptance has been claimed.


## Automated screening
{
  "task_id": "MAP-006",
  "decision": "submit_draft",
  "summary": "The draft spec at docs/map/specs/operations.md covers all nine required states (requested, authorised, queued, running, verifying, completed, failed, cancelled, recovery-required), timeout/unknown-outcome handling without inferring success from launch, retry/idempotency requirements with unresolved policy flagged, synthetic cases with undecided policy noted, and an explicit MAP-004 boundary that does not redefine the backup contract. The four coordinator-identified defects are corrected in the quoted draft: the queued row separates retry (No) from cancellation via a Cancellable? column; section 6.2 defers backup integrity-verification mechanics and pass/fail criteria to MAP-004; section 4.1 renames completed-at to finished-at (terminal only: completed, failed, cancelled); and section 6.1 fixes 'an reviewed' to 'a reviewed'. Baseline intent is separated from proposed schema rules, modality is preserved, no implementation/transport/tests are assumed or claimed, consent and backup-vs-restore boundaries are respected, and offline limitations plus preserved unknowns are documented. No findings remain; the draft may proceed to a draft PR (not acceptance).",
  "findings": []
}
