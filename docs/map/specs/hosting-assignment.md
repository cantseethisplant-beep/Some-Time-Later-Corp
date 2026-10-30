# Hardware Offers and Hosting Assignment Contract (MAP-003)

**Task:** MAP-003 — Define hardware offers and assignment fields
**Status:** proposed map specification; not accepted, not implemented
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md)
**Worker:** hermes-laptop-map003-repair-20261030
**Technology neutral:** no operating system, runtime, cloud provider, deployment tool, licence, cost, or implementation is selected here.

## 1. Purpose and scope

This specification proposes two locally owned record shapes: a hardware offer made by a hardware owner, and a hosting assignment proposed by an authorised manager and accepted within the owner's consent. It converts the Build Idea 2 journey in docs/CONCEPT.md into fields, states, and case handling without depending on another task schema.

Scope is bounded: no deployment runtime, host measurement, catalogue verification, pricing, or backup implementation. Backup and movement are referenced by policy identifier only; their procedures belong to separate accepted records. All examples are synthetic and illustrative.

**Provenance distinction.** Baseline intent comes from README.md (idea and boundaries), docs/CONCEPT.md (offer/assignment journey, dependency awareness), docs/DECISION-GUIDE.md (volunteer-hardware risks, open questions), and docs/TRUST-AND-RECOVERY.md (roles, hardware boundaries, backup and movement). Field lists, mandatory subsets, case states, and validation rules below are proposed design additions, not established baseline facts; items the baseline does not settle are marked "proposed" or "unresolved."

## 2. Locally defined terms

- **hardware owner** — a member who volunteers a computer, virtual machine, or limited resource allocation and sets the limits under which it may be used (baseline: CONCEPT.md step 2; TRUST-AND-RECOVERY.md hardware boundaries).
- **hardware offer** — the owner's recorded statement of available resources, permitted workloads, availability, expiry, timezone, movement window, and backup-policy reference (proposed field shape).
- **hosting assignment** — a manager's proposal to run a specific application version on a specific approved host, within the owner's offer limits, with its own expiry, movement window, backup schedule, destination, retention, and recovery custodians (baseline: CONCEPT.md hosting assignment; proposed field shape).
- **workload** — an application, add-on, or shared service; standalone applications, add-ons, and shared services are distinct, and placement must consider databases, background jobs, persistent data, and application-specific requirements (baseline: CONCEPT.md dependency awareness).
- **movement window** — the period during which moves may begin and end, including quiesce, state handover, destination verification, routing change, and fencing of the previous writer (baseline description: TRUST-AND-RECOVERY.md; exact fencing behaviour unresolved).
- **backup-policy reference** — a local identifier for a separate backup/restore record; this specification never embeds backup mechanics (proposed).
- **recovery custodian** — a privilege authorising retrieval or restoration of specifically authorised recovery material, separated from deployment/assignment authority (baseline: TRUST-AND-RECOVERY.md roles). Separation of privileges does not require two different people; final role policy is undecided.
- **proposed schema** — the field lists and validation rules here are local proposals requiring separate acceptance; they are not baseline requirements.

## 3. Hardware offer fields (proposed schema)

Every offer records:

1. **offer_id** — locally assigned identifier (proposed).
2. **owner_id** — the hardware owner whose consent grounds the offer (proposed).
3. **consent_scope** — workload types the owner permits; arbitrary remote commands and unrestricted host or personal-file access are out of scope (baseline intent: TRUST-AND-RECOVERY.md hardware boundaries; proposed field).
4. **consent_status** — active or revoked (proposed state field).
5. **resources** — offered resource categories, for example CPU, memory, storage, network, as the owner's limits; no units or stack-specific values are mandated (proposed).
6. **availability** — operating periods when the host is expected reachable, with timezone; absence of availability records offline periods, not guaranteed downtime (proposed).
7. **movement_window** — the window in which moves of hosted workloads may begin and end, with timezone (proposed).
8. **expiry** — the instant after which the offer is invalid for new assignments; what happens to active assignments at expiry is unresolved (proposed).
9. **backup_policy_ref** — reference to the owner-accepted backup/restore policy covering hosted workloads on this host (proposed).
10. **offered_at and last_revised_at** — timestamps with timezone (proposed).

**Proposed assignability rule.** Fields 1–10 must be present and consent_status active for an offer to be assignable. An incomplete offer may be recorded as draft/incomplete but no assignment may reference it until every required field and policy reference is supplied. Future fields such as cloud account credentials, spend limits, or automatic failover settings are out of scope and explicitly unresolved (proposed).

## 4. Hosting assignment fields (proposed schema)

Every assignment records:

1. **assignment_id** — locally assigned identifier (proposed).
2. **offer_id** — references an existing, valid hardware offer (proposed).
3. **application and version** — the application bundle and reviewed immutable version; add-ons and shared services listed separately where the bundle requires them (baseline intent: CONCEPT.md dependency awareness; proposed field).
4. **dependencies** — databases, background jobs, persistent data, and application-specific requirements placement must consider (proposed).
5. **resource_limits** — owner-approved limits drawn from the offer's resources; an assignment must not exceed them (proposed validation rule).
6. **operating_schedule** — when the workload may run, with timezone (proposed).
7. **assignment_expiry** — the instant after which the assignment is no longer authorised; renewal requires a new consent check against the current offer (proposed; re-consent default unresolved).
8. **movement_window** — inherited from or narrowed against the offer's movement window; moves outside it require re-consent (proposed).
9. **destination** — the approved host identity within this record system; not a network address or cloud endpoint (proposed).
10. **backup_schedule and backup_policy_ref** — scheduled or on-demand backups reference the same application-specific backup procedure; the backup record itself is separate (proposed).
11. **retention** — how long recovery copies are kept; the data-loss window is acknowledged, not eliminated (baseline intent: TRUST-AND-RECOVERY.md; proposed field).
12. **recovery_custodian** — the privilege authorised for recovery material, separated from the manager who created the assignment; not necessarily a different person (baseline intent: TRUST-AND-RECOVERY.md roles; proposed field).
13. **proposed_by, proposed_at, consent_confirmed_at, consent_confirmed_by** — manager and owner consent timestamps (proposed).

**Proposed required subset:** assignment_id, offer_id, application, version, resource_limits, assignment_expiry, recovery_custodian, and at least one of operating_schedule or movement_window. All other fields are optional pending separate policy records. These are proposed validation rules, not baseline-established requirements.

## 5. Consent, withdrawal, and case states

Owner consent is the gate. An owner may revoke future hosting at any time (baseline: TRUST-AND-RECOVERY.md hardware boundaries). Revocation does not by itself specify what happens to already running workloads; that handling is unresolved and must be reconciled against application-specific fencing and failure tests (baseline: DECISION-GUIDE.md open questions).

Case states (proposed):

- **valid** — offer present, not expired, consent active, resources sufficient, workload within consent scope.
- **invalid** — missing required field, expired offer, revoked consent, insufficient resources, workload outside consent scope, or nonexistent offer or backup policy reference. Invalid assignments must not be deployed.
- **withdrawn** — owner revoked consent after the assignment was valid. No new assignments may reference the offer. Existing workload migration, stop, or fencing requires an agreed application policy, authorised actors, and later evidence; this document promises neither instant deletion nor write fencing on an offline owner machine.
- **offline** — host not reachable during declared availability. An offline host cannot make a new backup, and recovery may lose changes since the most recent usable copy (baseline: TRUST-AND-RECOVERY.md). Offline is an operational observation, not consent revocation.

Transitions are events with timestamps and the actor or observation source (proposed). No automatic failover is assumed (baseline: TRUST-AND-RECOVERY.md). Withdrawal is distinct from observed node connectivity and from backup or movement operation success; no new assignments to a withdrawn offer.

## 6. Backup and movement references

Backup policy references point to separate accepted records. A clicked (manual) backup and a scheduled backup should use the same application-specific backup procedure as proposed in the baseline (CONCEPT.md pairing of a backup button and a timed backup); this specification names the procedure by reference only. Backup-copy verification and independent restore-test evidence are different things, and neither was performed in this drafting run; the procedure is not called "verified" here.

A movement window covers quiesce, state handover, destination verification, routing change, and fencing of the previous writer (baseline description). If verification fails, stop and use a tested rollback procedure; never allow two authoritative writers merely because both hosts appear healthy (baseline: TRUST-AND-RECOVERY.md). These behaviours are baseline intent, not implemented evidence.

## 7. Synthetic examples

These examples use no real corporation, host, application, or person data. They demonstrate field shape only. The required-field check is against the proposed subset in section 4.

**Example A — trusted host, authentication bundle (assignable, complete).**
- offer: owner-consented CPU, memory, storage; consent_scope limited to authentication and related services; availability with timezone; movement window aligned to a Sunday maintenance period; backup_policy_ref present; expiry set; all proposed required offer fields present.
- assignment: application version and dependencies listed; resource limits within the offer; movement window within the Sunday window; recovery_custodian privilege separated from the assigning manager's authority; all proposed required assignment fields present.
Mirrors the illustrative trusted-host example in CONCEPT.md; not a default.

**Example B — volunteer member host (incomplete, not assignable).**
- offer: limited resource allocation; availability outside the member's working hours with timezone; workload scope restricted to non-sensitive standalone applications; owner-set expiry. **Missing:** backup_policy_ref is not supplied, so under the proposed assignability rule this offer is draft/incomplete and no assignment may reference it.
- assignment: none proposed. If drafted, it would be invalid because it references an incomplete offer; sensitive tokens and authoritative databases belong on appropriately trusted infrastructure (baseline: TRUST-AND-RECOVERY.md hardware boundaries).

**Example C — invalid.**
- offer missing expiry or consent_scope; assignment requesting resources above the offer; workload outside consent scope; expired offer referenced; assignment referencing a nonexistent backup_policy_ref. Each case fails a proposed validity condition and must not be deployed.

**Example D — withdrawn (no write-fencing mandate).**
- assignment valid, then owner revokes consent → consent_status revoked, case state withdrawn. No new assignments may reference the offer. What happens to the running workload — stop, finish, rollback — is unresolved and requires application-specific fencing and failure tests plus authorised actors; this document mandates neither instant deletion nor write fencing on the owner's offline machine.

**Example E — offline.**
- host within declared availability but unreachable; case state offline (observation, not revocation); no new backup possible; recovery target prepared separately; automatic failover not assumed.

## 8. Reconciliation needs and unresolved decisions

Recorded as open, not resolved:

- What happens to running assignments when an offer expires or is withdrawn (stop, finish, rollback); requires application-specific fencing and failure tests.
- Which workloads are acceptable on volunteer hosts versus trusted infrastructure (DECISION-GUIDE.md open questions).
- Operating systems, deployment runtime, cloud provider, and spend-limit enforcement are unselected.
- Backup/restore evidence, restore exercises, and measured recovery time and data-loss targets are pending per application.
- Recovery custodian succession and emergency recovery procedures are undecided design decisions.
- Cloud integration is optional and unverified; no provider or cost is assumed.
- Exact mandatory subsets, expiry/renewal/re-consent defaults, and offer-level schedules are proposed here and not baseline-established.

## 9. Proposed-rule check list (corrections applied)

| Correction | Section | Check performed |
|---|---|---|
| Consistent assignability rule; backup_policy_ref not optional in examples | 3, 7 | One proposed assignability rule in §3; Example B explicitly incomplete/non-assignable due to missing backup_policy_ref; Example A complete; no example uses "optional" to bypass a mandatory rule. |
| Withdrawal does not mandate write blocking or instant deletion | 5, 7 | §5 states existing-workload handling is unresolved; Example D contains no write-fencing or instant-deletion promise; withdrawal separated from connectivity and operation success. |
| Contract labelled proposed; baseline intent cited by section | 1–8 | §1 separates baseline intent (cited per document) from proposed design; "every surfaceable fact traces" claim removed; proposed additions marked "proposed." |
| Manual and scheduled backup share one procedure; no "verified restore" claim | 4, 6 | §4 and §6 require the same application-specific backup procedure for manual and scheduled backups; restore-test evidence stated as not performed; no "verified restore procedure" wording. |
| No accidental mandates, contradictions, or custodian identity rule | 2, 4, 5 | recovery_custodian defined as separated privilege, not a different person; consent, availability, and execution distinct; no stack, provider, numerical defaults, or cross-schema dependency introduced. |

This document is planning text, not proof that anything works. It must not be treated as accepted until the project owner or an appointed reviewer integrates it against MAP-003 criteria.
