# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/7

Automated critic only; independent review pending.

# MAP-004 finished-work handoff

**Task:** MAP-004 — Specify backup and recovery outcomes
**Worker:** hermes-laptop-map004-20261030
**Commit:** a26a5e02f50815a1d94e39f76d6880b269aa7874 (task/claim commit; claim token dIoKBs0exZGqp20gSZvmfTjKXU02-wtP is a claim identifier only, not authorization or acceptance)
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e
**Branch:** hermes/map-004-20261030 (claimed, not created or pushed by this worker)
**Output produced:** docs/map/specs/backup-recovery.md (complete contents above)
**Claimed at / last activity:** 2026-10-30T02:10:23.064Z

## Exact sources

README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md, all at input revision 792b158838aa5214d0156690d24e21e780de542e. Source text was supplied in the task prompt; this worker did not re-fetch from a live repository and could not verify the live board or other revisions.

## Diagnosed issues and exact corrections

1. Section 2 previously loosely applied all five labels to every record type and framed Restore-tested as a Verified copy exit state, conflicting with Section 6's separate vocabularies. Correction: restated Section 2 so operations use Requested/Running/Verified copy/Failed; a retained copy carries Verified copy status with retention/supersession status; Restore-tested is a restore-exercise result category with sub-states attempted/succeeded/failed/not performed; a failed restore never becomes a copy state and never overwrites verified-copy evidence. Cited Section 2 and Section 6. Remaining uncertainty: none of these states is backed by an implemented system; which proposed design elements the coordinator will accept as settled is undecided.

2. Section 7 Example A previously omitted Section 6 restore-exercise record fields (custodian, data loss since most recent usable copy, time to recover, live routing/writers affected) without annotation and referenced operation/copy records without all Section 6 fields. Correction: annotated Example A as an abbreviated flow; O1 and C1 omit partial-copy flag, procedure version, superseded-by, removed-at; E1 omits custodian, data loss, time to recover, and result evidence, marked pending for the synthetic case; live routing/writers affected explicitly false for an isolated exercise. Cited Section 7 and Section 6. Remaining uncertainty: examples contain no implementation evidence.

## Checks actually performed

- Acceptance criteria mapped to spec sections: Section 2 (five separate outcomes by record type), Section 4 (unresolved values), Section 5 (restore-task evidence; no completed restore tests claimed), Section 9 (mapping table).
- Separated backup-operation state, retained-copy verification state, and restore-exercise result; transitions cover rejected requests, partial copies, failed restore, retention removal, and retry as a new operation (Sections 2 and 6).
- Removed planned-move steps (destination consent, routing switch, writer fencing, rollback) from routine backup rules; they appear only under rule 5 and are excluded from isolated restore exercises in Section 5.
- Separated baseline intent from proposed design (Section 1); Section 6 record concepts labelled proposed design; sources cited per rule in Sections 2–4.
- Distinguished restore-exercise results attempted/succeeded/failed/not performed; a successful upload or integrity check does not prove recoverability; a failed restore leaves a visible failure and no success certification.
- Text-checked Example A and Example B against Section 6 record rules; Example A annotated with omitted fields and pending custodian/data loss/time-to-recover; live routing/writers affected=false; no timing, provider, or numerical defaults invented; no unresolved policy mandated in examples.
- Confirmed no external writes, no tool use beyond supplied inputs, no self-acceptance; output limited to docs/map/specs/backup-recovery.md.

## Limitations

- No GitHub, terminal, network, or delegation tools available; inputs read from prompt text only.
- Baseline is user intent only, with no upstream technical verification; no storage vendor, encryption implementation, operating system, or cost selected.
- This worker performed no backup/restore test and claims none; nothing asserts the absence of evidence outside the supplied inputs.
- Unresolved values remain decisions for later: custodian access rules, key-separation implementation, offline-host behaviour, retention, per-application data-loss and recovery targets.

## Remaining work

- Coordinator or user submits the finished-work packet via the GitHub submission issue form; submission is not acceptance.
- Unresolved values require decisions before implementation.
- A later restore task must supply Section 5 evidence and perform an actual restore exercise.

## Review pending

Yes — this specification awaits coordinator/project owner review and acceptance against MAP-004 acceptance criteria. The claim is not released; no new work is undertaken.


## Automated screening
{
  "task_id": "MAP-004",
  "decision": "submit_draft",
  "summary": "The draft satisfies MAP-004 acceptance criteria: Section 2 separates operation labels (Requested/Running/Verified copy/Failed), retained-copy status (Verified copy with retention/supersession), and Restore-tested as a restore-exercise result category (attempted/succeeded/failed/not performed) without collapsing vocabularies or letting a failed restore become a copy state; Section 4 leaves custodian access, key-separation implementation, offline-host behaviour, retention, and per-application data-loss/recovery targets unresolved and explicitly non-mandatory; Section 5 defines the evidence a later restore task must supply and states no completed restore test is claimed; Section 6 labels record shapes as proposed design; Example A is annotated as abbreviated with omitted Section 6 fields marked pending and live routing/writers affected=false; no storage vendor, encryption implementation, or test is claimed. No precise actionable findings remain; this permits a draft PR, not acceptance.",
  "findings": []
}
