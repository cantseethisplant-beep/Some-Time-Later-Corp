# MAP-035 Candidate Blueprint — CANDIDATE — NOT ACCEPTED OR BUILD-READY

**Task:** MAP-035 — Integrate recovered assembly parts into the candidate blueprint
**Claim commit:** 73f760be501bf158eab31d8b4df7c0914fc3b74b
**Worker:** hermes-laptop-map-035-auto-20261030
**Output path:** docs/map/specs/loop-map-035-candidate.md
**Status:** candidate draft for review only. Not accepted, not build-ready, no app implemented or tested, no deployment claimed.

## 1. What this document is and is not

This is the consolidated candidate blueprint for the recovered-source integration task MAP-035. It links the three newly published recovered assembly parts (MAP-031, MAP-032, MAP-033) into one navigable map, states what a builder can plan from now, and names exactly which checks block a verified build.

It is not accepted work, not an architecture certification, and not permission to implement, deploy, spend, or select a stack. No owner decision is resolved here. No upstream identity, version, or licence is verified. No test, restore exercise, or deployment is claimed.

All three recovered parts are unaccepted coordinator-corrected draft parts: synthesis inputs, not established technical evidence. They are linked below as appendices by exact immutable path and revision; their full text is not copied here.

## 2. Navigation index

1. Section 3 — Published recovered parts (appendix links, roles, evidence status).
2. Section 4 — Baseline intent, proposed designs, and unaccepted coordinator corrections.
3. Section 5 — Bounded proposed MVP and exclusions.
4. Section 6 — Logical component/data/interface overview (summary; full map in Appendix B).
5. Section 7 — Ordered implementation path (numbered build actions B01–B14 with observable checks).
6. Section 8 — Requirement-to-step-to-check crosswalk (REQ-01..REQ-17 → steps → AM checks).
7. Section 9 — Enrolment/authority/trust boundaries.
8. Section 10 — Operations/scheduling/deployment/release/rollback and backup/restore path.
9. Section 11 — Source-linked owner/evidence prerequisites and unresolved conditions.
10. Section 12 — Blockers to a verified build.
11. Section 13 — Limitations and review pending.

## 3. Published recovered parts (linked appendices)

These are the new source set for MAP-035. The original MAP-034 did not have them as inputs. They are reviewed draft material only.

- **Appendix A — Build sequence and requirement traceability:** `docs/map/specs/loop-map-031-assembly.md` @ `f72e9b995af03cd88cc096c0146186595da33f0d` (source task MAP-031). Defines stages A–C, steps B01–B14 in prerequisite order, and the REQ-to-step traceability table.
- **Appendix B — Component/data/interface map:** `docs/map/specs/loop-map-032-assembly.md` @ `c426a685a2c40bd74a2a4db63acb645d3e210d85` (source task MAP-032). Logical controller/node/adapter/corporation map, entity glossary, relationship crosswalk, interface table, trust/decryption boundaries.
- **Appendix C — Acceptance and evidence matrix:** `docs/map/specs/loop-map-033-assembly.md` @ `90c954ddeb85b66508c668039244791a689ce629` (source task MAP-033). AM-* check inventory across 13 areas, decision register OD-01..OD-14, MAP-015 release/rollback verification context as unaccepted candidate only.

No part is consumed as accepted requirements, dependency satisfaction, or verified technical evidence. A blocked part would be listed explicitly and never used as evidence; none of the three is blocked.

## 4. Baseline intent, proposed designs, and unaccepted coordinator corrections

Three layers are kept separate throughout this blueprint:

- **Baseline intent:** the four concept inputs at `792b158838aa5214d0156690d24e21e780de542e` (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md). User intent only; no upstream technical verification.
- **Proposed designs:** field schemas, state models, step IDs, check IDs, and boundary rules added by MAP-001 through MAP-015, MAP-017 through MAP-027, and the recovered assembly parts. Pending separate acceptance; never treated as baseline musts.
- **Unaccepted coordinator corrections:** the replacement wording in MAP-023/MAP-026 (enrolment requires consent, immutable version, and measured resources only; restore-before-approval is proposed design, not a baseline gate) and the MAP-031..033 assembly framing. These are disclosed as corrections, not adopted mandates.

No example in this document upgrades an unresolved policy into a mandate.

## 5. Bounded proposed MVP and exclusions

**In scope for the candidate plan:** role matrix, catalogue entry states, hardware-offer and assignment field shapes, eight node lifecycle states, operation status model, time semantics, dependency-aware placement, controlled deployment preparation, release lifecycle stages, backup creation distinct from restore verification, planned move and fencing, recovery-custodian access boundaries, and the B01–B14 implementation path.

**Explicitly excluded:** technology stack, operating system, deployment runtime, cloud provider, licence selection; cost figures, spend limits, retention values; component, integration, or restore tests; runtime verification; Discord integration that duplicates existing Discord communication; automatic failover; infrastructure provisioning or deployment execution; any external write.

The MVP is bounded to one controlled hosting target on volunteered hardware with scheduled and manual backups; multiple hosts, service movement beyond the planned-move procedure, failover, and cloud provisioning are later capabilities, not part of this candidate.

## 6. Logical component/data/interface overview (summary)

Full detail is in Appendix B. The logical map has four zones:

- **Corporation:** CEO, appointed managers, hardware owners, members, recovery custodians. Administration and recovery contacts are recorded before assignments (baseline intent).
- **Controller:** the platform itself; holds catalogue, offer, assignment, and operation records. Needs its own reliable storage and hosting; workloads should keep running during controller outages subject to their own dependencies — must be tested, not assumed. Automatic failover is a later capability.
- **Node/host:** volunteered computer, VM, or limited allocation. Eight proposed lifecycle states: offered → enrolment-pending → approved → active → disconnected → draining → revoked → retired. Revocation (management-access removal) is distinct from verified workload/data cleanup.
- **Adapter:** application-specific deployment, movement, backup capture, and restore verification logic; not selected here.

Data relationships (proposed): catalogue entry → hosting assignment via bundle role and dependencies; hardware offer → assignment via offer_id with resource_limits within offer resources; each assignment action is an operation with a lifecycle state; backup operations use MAP-004 outcome labels and restore exercises are separate evidence items — restore_verified is never derived from a backup upload.

Interface boundaries preserved: deployment authority separate from backup decryption permission (who may decrypt is unresolved); movement authorisation requires destination consent and compatibility; recovery-custodian access limited to authorised material; operation status reporting does not redefine the MAP-004 backup contract.

## 7. Ordered implementation path (numbered logical build actions)

Reusing the stable step IDs from Appendix A, in prerequisite order:

**Stage A — Foundation and boundaries**
1. **B01** — Controller boundary and roles matrix; separate deployment authority from backup decryption permission. Inputs: TRUST-AND-RECOVERY roles; DECISION-GUIDE open questions; MAP-002 matrix. Observable check: matrix lists five roles and seven actions; unresolved owner decisions marked unresolved.
2. **B02** — Catalogue entry states and evidence conditions (proposed schema only). Observable check: four states present; backup fields and restore fields separate.
3. **B03** — Hardware offer and assignment field inventories (proposed schema only). Observable check: proposed assignment required subset explicit; missing backup_policy_ref makes an offer draft/incomplete.
4. **B04** — Enrolment and withdrawal lifecycle states. Observable check: revocation separated from verified cleanup; identity/key mechanism marked unresolved.
5. **B05** — Operation status model and failure reporting. Observable check: success never inferred from launch; recovery-required distinct from failed.
6. **B06** — Time semantics for schedules, expiry, and movement windows. Observable check: no default timezone or schedule invented; missed-schedule policy unresolved.

**Stage B — Deployment and catalogue placement**
7. **B07** — Dependency-aware placement rules. Observable check: entry type populated before placement; dependency_evidence unresolved where unconfirmed.
8. **B08** — Controlled deployment preparation and verification step. Observable check: deployment verification passes on target host before assignment is active — proposed, not independently verified.
9. **B09** — Release lifecycle stages and rollback limits. Observable check: superseded release retained for rollback; rollback reason/procedure/outcome recorded if used.
10. **B10** — Backup creation distinct from restore verification. Observable check: upload success not recast as recoverability; failed restore does not overwrite verified-copy evidence.

**Stage C — Movement, reporting, recovery, and rollout**
11. **B11** — Planned move and fencing procedure. Observable check: two authoritative writers never admitted merely because both hosts appear healthy.
12. **B12** — Operation reporting and idempotency for moves/backups/deploys. Observable check: unknown outcome not auto-retried; launch alone never infers completion.
13. **B13** — Recovery-custodian access boundaries and emergency recovery outline. Observable check: decryption authority not assigned; custodian succession unresolved.
14. **B14** — Repeatable rollout isolation principle (unsourced REQ-16 scope). Observable check: REQ-16 marked unsourced/proposed-design-only; no baseline modality invented.

This is proposed sequencing only, not an accepted architecture.

## 8. Requirement-to-step-to-check crosswalk

REQ-01 through REQ-17 come from the MAP-001 draft (unaccepted review material); status/modality labels are consolidation labels only.

| REQ | Behaviour | Step(s) | AM check | Flagged? |
|---|---|---|---|---|
| REQ-01 | Administration and recovery contacts/custodians recorded | B01, B13 | AM-REQ-01, AM-ROLES-01 | No |
| REQ-02 | Members offer hardware with availability and workloads | B03 | AM-REQ-01 | No |
| REQ-03 | Managers choose reviewed bundle; inspect dependencies/resources | B07, B08 | AM-REQ-01 | No |
| REQ-04 | Assignment within owner consent and limits | B03, B08 | AM-REQ-01 | Hard "must not exceed" gate is proposed-design |
| REQ-05 | Controlled deployment prepared and verified before use | B08 | AM-BA-01 (candidate context) | Verification proposed, not verified |
| REQ-06 | Users monitor health; request or schedule backups | B05, B10 | AM-OPS-01 | No explicit should for health exposure |
| REQ-07 | Movement/recovery procedure records outcome and attention items | B11, B12 | AM-REQ-01 | No |
| REQ-08 | Assignment record fields incl. retention and recovery custodians | B03 | AM-REQ-01 | Retention and exact times undecided (OD-14) |
| REQ-09 | Manual and scheduled backups share one procedure | B10 | AM-RCV-01 | Identical execution not evidenced |
| REQ-10 | Hardware and optional cloud resources recorded; no cost targets preset | B02 | AM-CST-01 (gap) | Optional cloud recording; no spend limit assumed |
| REQ-11 | Catalogue marks standalone/add-on/shared service | B02 | AM-CAT-01 | Entry type before placement is proposed design |
| REQ-12 | Placement considers databases, jobs, persistent data | B07 | AM-CAT-01 | Placement validation rule is proposed design |
| REQ-13 | No Discord duplication | None yet | N/A | Flagged: exclusion boundary, no build step |
| REQ-14 | "Supported" only after full evidence set | B02 | AM-CAT-01 | Upstream verification pending |
| REQ-15 | Consistent protected backup; integrity verified; keys separate | B10 | AM-RCV-01 | Backup behaviour not technically verified |
| REQ-16 | Rollout to second isolated corporation | None (B14 records principle only) | AM-REQ-01 | Flagged: unsourced row retained |
| REQ-17 | Owner may withdraw; recorded; no new assignments; no instant deletion | B04 | AM-NS-01 | Offline mechanics unresolved (OD-07) |

Requirements with no implementable step yet: REQ-13 and REQ-16.

## 9. Enrolment/authority/trust boundaries

Following the unaccepted MAP-023/MAP-026 replacement wording (proposed design, not baseline mandate): enrolment (offered → approved) requires hardware owner consent, application reviewed immutable version, and measured resources only. Demonstrated recoverability is assignment-readiness or owner policy, not an enrolment gate.

- CEO appoints managers and recovery custodians; approves critical policy. Succession must not silently grant access to every historical secret.
- Appointed managers manage only explicitly delegated applications and assignments.
- Hardware owners consent to workloads within their offer and may revoke future hosting; revocation affects future hosting and does not itself undo an in-flight assignment or promise instant deletion on an offline machine.
- Deployment authority and permission to decrypt backups are separate; who may decrypt is unresolved (OD-11).
- Recovery custodians retrieve or restore specifically authorised recovery material only; separation of privileges does not require two different people; final role policy is undecided.

## 10. Operations/scheduling/deployment/release/rollback and backup/restore path

Operations use the nine-state model (requested → authorised → queued → running → verifying → completed → failed → cancelled → recovery-required); timeout produces an unknown outcome, never auto-retried; idempotency keys required for retried operations. Scheduling semantics treat a movement window as a time-based permission, not a migration promise; missed schedules are not silently caught up; clock skew is tolerated in fencing.

Deployment: reviewed immutable version checked against host runtime; resource limits within owner offer; verification on target host before assignment active. Release lifecycle: proposed → reviewed → approved-for-environment → deployed → superseded → withdrawn; rollback reason/procedure/outcome recorded; no two authoritative writers.

Backup/restore: backup operation labels Requested/Running/Verified copy/Failed; restore exercise categories attempted/succeeded/failed/not performed. A successful upload is not proof of recoverability; a restore exercise is required; keys are managed separately from encrypted copies. No restore test exists or is claimed in this repository.

## 11. Source-linked owner/evidence prerequisites and unresolved conditions

Owner decisions (none resolved here):
- OD-01 Who operates and pays for the central controller (DECISION-GUIDE open questions).
- OD-02/OD-10 CEO identity, delegation, succession, emergency recovery (DECISION-GUIDE; TRUST-AND-RECOVERY roles).
- OD-03 Volunteer-host workload acceptability vs trusted infrastructure.
- OD-04 OS, deployment runtime, cloud provider for the pilot.
- OD-05 Cloud spending-limit enforcement and over-capacity behaviour.
- OD-06 Recovery time and data-loss targets per application.
- OD-07 Hardware-owner withdrawal while the machine is offline.
- OD-08 Who may read each corporation data type; how consent is documented.
- OD-09 Product licensing and distribution model (no reuse licence selected; README project boundaries).
- OD-11 Decryption authority separate from deployment; who may decrypt.
- OD-13 Automatic failover evidence required before assumption.
- OD-14 Retention and exact times for assignment fields.

Upstream evidence (none verified): identity, version, licence for any catalogue candidate — Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures, CorpTools. A GitHub listing alone proves none of these. No pinned reviewed immutable versions; no measured resources; no component, integration, or restore tests performed or claimed.

## 12. Blockers to a verified build

A verified build is blocked until the following are resolved with evidence, not assumptions:

1. Owner decisions OD-01 through OD-14 above, especially controller operator/pay, succession/emergency recovery, volunteer-workload policy, stack/provider, spend limits, RTO/RPO, offline withdrawal, data consent, product licence.
2. Upstream identity/version/licence verification for at least one application bundle intended for the pilot.
3. Measured resources and dependency evidence for the bundle (database, background jobs, persistent data).
4. Restore-exercise evidence for the bundle; backup creation does not substitute for restore verification.
5. Planned-move and fencing evidence per application; no two authoritative writers rule must be demonstrable.
6. Controller outage behaviour must be tested; automatic failover excluded pending its own evidence.

These are precise prerequisites, not a generic list of unknowns. Numbered build actions B01–B14 remain plannable now, but none can reach acceptance without the checks above.

## 13. Limitations and review pending

All inputs are user-intent baseline or unaccepted completed drafts; genuinely verified evidence is empty. Board state and file SHAs were not independently verified; no GitHub, terminal, network, or delegation tools are available. No stack, provider, cost, licence, retention value, owner, date, test, or deployment is invented or claimed. This document is review input only; acceptance rests with the project owner or an appointed reviewer; nothing is self-accepted. Up to two document corrections may apply under task policy.

Review pending: yes — coordinator/owner review required.
