# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/9

Automated critic only; independent review pending.

## MAP-007 Handoff (coordinator tracking record)

**Task:** MAP-007 — Define scheduling and time semantics
**Worker:** hermes-laptop-map-007-auto-20261030
**Claim commit:** f2d08b1f1b9886cd97a263d47978fedd1da2e45e
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e
**Output path:** docs/map/specs/scheduling.md
**Status:** drafted; corrected per coordinator feedback; not submitted, not accepted; claim not released

### Sources used
README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md — all at revision 792b158838aa5214d0156690d24e21e780de542e. Evidence type: user-intent baseline; no upstream technical verification.

### Diagnosed issues and exact corrections

Issue 1 — §6 Example 2 stated "After expiry the platform must not accept new writes for that assignment," a write-blocking expiry rule invented from outside the pinned inputs and contradicting §7 open question "Whether assignment expiry blocks reads, writes or both."
Correction: Example 2 reworded so expiry carries a stored instant with storage convention unresolved (§3.1, §7), expiry semantics explicitly undecided, and outcomes framed as possibilities ("A policy may block writes after expiry, may block reads and writes, or may take no access action at all; this specification selects none of those outcomes"). Cross-reference to §7 added; expiry is not a movement trigger and does not start a migration.

Issue 2 — §3.1 proposed "display times in the explicit timezone of the requesting user or corporation policy," selecting default display rules not present in the inputs.
Correction: §3.1 narrowed to UTC storage intent only, labeled an unresolved proposal for MAP-003 review; display-time handling listed as unresolved with candidate rules (requesting user's timezone, corporation policy timezone, UTC) and none selected; explicit statement that no default timezone is invented.

### Checks actually performed
- Acceptance criterion 1: §3 covers UTC storage/display intent (3.1), explicit timezones (3.2), daylight-saving ambiguity (3.3), missed schedules (3.4), and clock uncertainty (3.5).
- Acceptance criterion 2: §4 separates a permitted movement window from a promise of successful automatic migration; automatic migration remains evidence-pending.
- Acceptance criterion 3: §6 provides four boundary examples; each references schematic field names only; required/optional status owned by MAP-003; no scheduling library selected; no defaults invented.
- Every example compared against required fields: all use schematic field names pending the MAP-003 registry; none establishes a default or mandates unresolved policy.
- Unresolved policy checked for accidental mandates elsewhere: Example 2 no longer imposes write-blocking expiry; §3.1 no longer proposes a default display rule; all §7 questions remain non-mandates.
- Backup creation versus restore verification kept distinct in §5; restore evidence is not inferred from backup completion.
- Optional/required distinctions preserved: field registry deferred to MAP-003; examples marked schematic and non-normative.
- Approximate word count within the 1,200–1,800 target.

### Limitations
- No GitHub, terminal, network or delegation tools were available; the live board, production instructions and MAP-003 field registry could not be re-read beyond the supplied prompt.
- No file write/read-back verification was possible; this is a drafted file section only.
- Inputs are concept baseline, not technical compatibility evidence; no upstream software identity, version, licence, cost or test was verified.
- No scheduling-library evaluation or measured restore-exercise evidence performed; out of scope.

### Remaining work
- Coordinator claim verification and board update; claim release before any new task.
- Alignment of §6 schematic field names with the MAP-003 field registry once it exists.
- Resolution of the §7 policy questions (storage convention, DST handling, missed-schedule policy, clock skew tolerance, expiry semantics, display-time rule).
- Scheduling-library decision, measured restore-exercise evidence, and automatic-movement/failover evidence in later tasks.

### Review pending
This submission is not acceptance. Review pending against MAP-007 acceptance criteria by the coordinator or project owner.


## Automated screening
{
  "task_id": "MAP-007",
  "decision": "submit_draft",
  "summary": "The corrected scheduling specification satisfies all three acceptance criteria. Section 3 covers UTC storage intent as an unresolved proposal rather than a baseline mandate, explicit timezones, daylight-saving spring-forward/fall-back ambiguity, missed-schedule policy with no silent double execution, and clock uncertainty with skew tolerance deferred to MAP-003. Section 4 clearly separates a movement window as time-based permission from any promise of successful automatic migration, keeping automatic migration evidence-pending. Section 6 provides four schematic boundary examples using field names pending the MAP-003 registry, with no scheduling library selected and no defaults invented; Section 7 preserves all policy questions as non-mandates. Baseline intent from the pinned inputs is separated from proposed semantics throughout, backup creation remains distinct from restore verification, and the two coordinator-flagged defects are corrected: Section 6 Example 2 no longer imposes write-blocking expiry and defers expiry semantics to the open question, and Section 3.1 no longer proposes a default display rule, listing candidate display rules with none selected. No unsupported facts, tests, implementation claims, or external research are introduced.",
  "findings": []
}
