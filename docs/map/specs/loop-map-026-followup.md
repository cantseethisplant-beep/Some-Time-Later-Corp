# Node Enrolment Gate and Restore-Proof Evidence — MAP-026

## 1. Purpose, claim, and evidence status

Task MAP-026 reconciles the node enrolment gate in docs/map/specs/node-lifecycle.md section 5 with restore-proof evidence in docs/map/specs/backup-recovery.md sections 5 and 8, against the baseline in docs/TRUST-AND-RECOVERY.md. The disputed point: MAP-014 section 5 lists "Backup/restore evidence: A tested restore exercise must exist" as trust evidence required before a node transitions from offered to approved, presenting it as baseline-derived. This document adopts the MAP-023 proposed replacement wording (docs/map/specs/loop-map-023-followup.md section 4): enrolment requires hardware owner consent, application reviewed immutable version, and measured resources only; demonstrated recoverability is separated as assignment-readiness/owner-policy and is explicitly proposed, not baseline-mandated.

This is a review-only reconciliation note. No edits are made to any original draft here; no policy is chosen; no software is implemented; no test is claimed. All referenced drafts are unaccepted completed drafts for review only; they are not accepted requirements, dependency satisfaction, or technical evidence. Evidence type: user-intent baseline; no upstream technical verification.

Claim: MAP-026; worker hermes-laptop-map-026-auto-20261030; claim commit 84f33db7dc5cade0e9f0739d5a2d40341852eeb1; input revision 792b158838aa5214d0156690d24e21e780de542e; loop policy 1, loop kind follow-up, loop cycle 3, area node-security, key node-approval-restore-proof-boundary.

### Source inventory (exact revisions)

- README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md @ 792b1588... — user-intent baseline; no upstream technical verification.
- docs/map/specs/node-lifecycle.md @ 39981db00918b363bc50f33cdb2dfe2dec22d210 — MAP-014 draft; section 5 in scope.
- docs/map/specs/backup-recovery.md @ ccf0957af0d80fe4608fc08b06b02408b485b1ca — MAP-004 draft; sections 5 and 8 in scope.
- docs/map/specs/loop-map-023-followup.md @ 810cc1f9ad0dc411977f3d37ba8b37e6e1980359 — MAP-023 proposed replacement wording; section 4 adopted as proposed design only.

## 2. Conflicting passages quoted

### Baseline: docs/TRUST-AND-RECOVERY.md @ 792b1588..., "Backup and movement"

"A successful upload is not proof of recoverability; a restore exercise is required."

"A backup is not a live standby. An offline host cannot make a new backup. Recovery may lose changes since the most recent usable copy."

The baseline asserts that a restore exercise is required to prove recoverability and denies that a successful upload is proof of recoverability. It does not state where in a node lifecycle that evidence must appear, and it does not make restore proof a condition of node enrolment or node approval. Owner policy (who decides, when, under what conditions) and workload acceptability remain open questions in docs/DECISION-GUIDE.md.

### MAP-014: docs/map/specs/node-lifecycle.md @ 39981db0..., section 5, "Trust Evidence and Unresolved Identity/Key Mechanism"

"The following trust evidence is required before a node may transition from offered to approved:

- Backup/restore evidence: A tested restore exercise must exist for the assigned application bundle; a successful backup upload is not proof of recoverability. (TRUST-AND-RECOVERY.md.)"

This converts the baseline's recoverability-proof statement into a node-enrolment/approval gate: restore-before-approval. No baseline passage prescribes restore-before-approval. The draft presents this as baseline-derived trust evidence without labelling it proposed design, which conflicts with MAP-004's position that restore evidence is supplied by "a later task" and that results include the category "not performed."

### MAP-004: docs/map/specs/backup-recovery.md @ ccf0957af..., section 5, "Evidence a later restore task must supply"

"Restore-exercise results are separated: attempted, succeeded, failed, not performed. A successful upload or integrity check does not prove recoverability; a failed restore leaves a visible failure and no success certification. This specification claims no completed restore tests; this evidence list is not evidence that any restore has been performed."

### MAP-004 section 8, "Limitations"

"This worker performed no backup or restore test and claims none; nothing here asserts the absence of evidence outside the supplied inputs."

## 3. Comparison: baseline intent vs the disputed approval gate

Baseline intent: restore exercise required to prove recoverability; successful upload not proof of recoverability. The baseline is silent on lifecycle placement and on restore-before-approval as an enrolment condition.

Disputed gate: MAP-014 section 5 makes a tested restore exercise a precondition of offered → approved. That is not in the baseline. It also conflicts with MAP-004 section 5, which frames restore evidence as something a later restore task must supply and explicitly lists "not performed" as a valid result category.

Disposition: enrolment prerequisites are reduced to consent, immutable version, and measured resources. Restore-proof is removed as a claimed baseline gate and is instead described as assignment-readiness / owner-policy, explicitly proposed design. No policy choice about whether, when, or how restore gating applies is made here.

## 4. Proposed replacement wording for MAP-014 section 5

The following is proposed replacement wording only. It is not baseline text, not accepted policy, and not an implementation. It adopts the MAP-023 section 4 wording as a proposal; any restore-before-approval policy introduced here is explicitly proposed, not baseline-mandated. Owner policy decisions remain unresolved.

### 5. Trust evidence and enrolment boundaries

Node enrolment and approval (offered → approved) require:

- Hardware owner consent: explicit, recorded consent to the specific assignment, including resource limits, acceptable workload types, operating schedule, and movement window (TRUST-AND-RECOVERY.md, "Proposed roles").
- Application reviewed immutable version: upstream repository and licence, reviewed immutable version, maintenance status (DECISION-GUIDE.md, "Catalogue entry requirements").
- Measured resources: the resource offer measured and recorded; no over-subscription beyond the hardware owner's stated limits (CONCEPT.md; DECISION-GUIDE.md).

No restore-exercise precondition is part of enrolment or approval in this wording. Whether recoverability evidence is required before assignment, before activation, or before production use is an owner policy decision and is left unresolved.

Assignment readiness (distinct from enrolment):

- The assignment stays within owner consent and approved limits; only predefined approved workloads may be assigned; resource limits must not exceed the offer (TRUST-AND-RECOVERY.md, "Hardware boundaries").

Demonstrated recoverability (restore proof; distinct from enrolment):

- A restore exercise is required to prove recoverability; a successful backup upload or integrity check is not proof of recoverability (TRUST-AND-RECOVERY.md, "Backup and movement").
- Restore-exercise result categories are attempted, succeeded, failed, not performed. A failed restore leaves a visible failure and no success certification (MAP-004 §5).
- Evidence for a restore exercise — source input revision, restore procedure version, verified copy used, target, steps performed, observed result, custodian — is supplied by a later restore task (MAP-004 §5). MAP-026 claims no restore test was performed.
- Backup integrity (a consistent recovery package protected in transit and at rest, integrity verified) is distinct from restore verification (a restore exercise result). One does not imply the other (MAP-004 §2, §5).

Any policy stating that a restore exercise must exist before node approval is explicitly proposed design in this document; it is removed as a claimed baseline gate. The baseline restore-exercise requirement for proof of recoverability remains intact.

## 5. Restore-exercise result categories retained via MAP-004 cross-reference

The result categories attempted, succeeded, failed, and not performed are retained exactly as defined in docs/map/specs/backup-recovery.md section 5, and the statement that no restore test was performed is retained from section 8:

- **attempted**: a restore exercise was run; outcome recorded per exercise.
- **succeeded**: the restore exercise completed successfully; evidence recorded.
- **failed**: the restore exercise failed; visible failure, no success certification.
- **not performed**: no restore exercise has been run; this is a valid result category, not a silent pass.

MAP-004 section 8: "This worker performed no backup or restore test and claims none; nothing here asserts the absence of evidence outside the supplied inputs." This record is preserved without modification.

Backup integrity vs restore verification: backup integrity (consistent recovery package, protected in transit and at rest, integrity verified) is a copy-lifecycle property; restore verification is a restore-exercise result. One does not imply the other (MAP-004 §2, §5).

## 6. Source/modality crosswalk

| Claim | Baseline (792b1588...) | MAP-014 §5 draft | MAP-026 disposition |
|---|---|---|---|
| Restore exercise required to prove recoverability | Stated intent | Repeated, attributed to baseline | Retained intact; not an enrolment gate |
| Tested restore exercise must exist before offered→approved | Not stated | Listed as required trust evidence | Removed as claimed baseline gate; restore-before-approval labelled proposed design only |
| Successful upload is not proof of recoverability | Stated | Repeated | Retained intact |
| Restore-exercise results include "not performed" | Not in baseline | MAP-004 §5 only | Retained via MAP-004 §5 and §8 cross-reference |
| Owner policy on restore-gating approval/assignment | Unresolved | Unaddressed | Left unresolved |

Restore-before-node-approval is either explicitly proposed here (as an option for owner decision) or removed as a claimed baseline gate; the restore-exercise requirement for proof of recoverability remains intact.

## 7. Distinctions preserved

- Baseline intent vs proposed design vs completed unaccepted reference drafts vs genuinely verified evidence: baseline intent is the four pinned concept documents @ 792b1588... (product intent only, no technical verification); proposed design is the MAP-026 replacement wording for MAP-014 section 5 and the explicit "proposed" labelling of restore-before-approval (pending separate acceptance, not adopted here); completed unaccepted reference drafts are MAP-014 @ 39981db0... and MAP-004 @ ccf0957af... (review material only; the contradiction is identified, not resolved as fact); genuinely verified evidence is none (no restore test, component test, or integration test exists in the supplied inputs, and none is claimed).
- Node enrolment/approval vs assignment authorisation vs demonstrated recoverability: three separate concerns.
- Backup integrity vs restore verification: a verified copy is not a restore-tested copy; restore-exercise evidence is a separate record concept.
- Desired test vs performed evidence: MAP-004 sections 5 and 8 record that no restore test was performed; evidence remains "not performed" unless a later task supplies it.
- Modality: baseline modal verbs are preserved; proposed design is never upgraded into a baseline mandate; unresolved owner policy is not resolved in examples.

## 8. Limitations and review pending

No GitHub, terminal, network or delegation tools are available; board state and file SHAs were not independently verified. No upstream technical verification, software licence, test, implementation detail, cost, or chosen stack is claimed or invented. Owner policy decisions (restore-gating timing, decryption authority, withdrawal while an offline host) remain unresolved. This document is a review input only; acceptance rests with the project owner or an appointed reviewer. Nothing is self-accepted.

Remaining work: coordinator or owner review of this draft; up to two document corrections may apply under task policy; acceptance and any merge remain with the project owner or appointed reviewer. Review pending: yes.
