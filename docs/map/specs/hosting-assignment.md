# Hardware Offers and Hosting Assignment Contract

**Task:** MAP-003 — Define hardware offers and assignment fields  
**Status:** proposed map specification; not accepted, not implemented  
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md)  
**Claim commit:** ff0476b4d8794f24ca0ec09675254ba6631825bd  
**Worker:** hermes-laptop-map003-20261030  
**Technology neutral:** no operating system, runtime, cloud provider, deployment tool, licence, or cost is selected here.

## 1. Purpose and scope

This specification defines two locally owned record shapes: a hardware offer made by a hardware owner, and a hosting assignment proposed by an authorised manager and accepted within the owner's consent. It converts the Build Idea 2 journey in docs/CONCEPT.md into fields, states, and case handling without depending on another task schema.

Scope is intentionally bounded. This file does not select a deployment runtime, measure any host, verify any catalogue application, set prices, or define backup implementation. Backup and movement are referenced by policy identifier only; their procedures belong to separate accepted records. All examples are synthetic and illustrative.

## 2. Locally defined terms

- hardware owner — a member who volunteers a computer, virtual machine, or limited resource allocation and sets the limits under which it may be used (CONCEPT.md step 2; TRUST-AND-RECOVERY.md hardware boundaries).
- hardware offer — the owner's recorded statement of available resources, permitted workloads, availability, expiry, timezone, movement window, and backup-policy reference.
- hosting assignment — a manager's proposal to run a specific application version on a specific approved host, within the owner's offer limits, with its own expiry, movement window, backup schedule, destination, retention, and recovery custodians (CONCEPT.md hosting assignment).
- workload — an application, add-on, or shared service. Standalone applications, add-ons, and shared services are distinct; placement must consider databases, background jobs, persistent data, and application-specific requirements (CONCEPT.md dependency awareness).
- movement window — the period during which an application may be moved to another host, including quiesce, state handover, destination verification, routing change, and fencing of the previous writer (TRUST-AND-RECOVERY.md backup and movement).
- backup-policy reference — a local identifier for a separate backup/restore record; this specification never embeds backup mechanics.
- recovery custodian — a person authorised to retrieve or restore specifically authorised recovery material, separate from deployment authority (TRUST-AND-RECOVERY.md proposed roles).

## 3. Hardware offer fields

Every offer records:

1. offer_id — locally assigned identifier.
2. owner_id — the hardware owner who consented; consent is required before any assignment references this offer.
3. consent_scope — the workloads the owner permits, by workload type; arbitrary remote commands and unrestricted host or personal-file access are out of scope (TRUST-AND-RECOVERY.md hardware boundaries).
4. resources — offered resource categories, for example CPU, memory, storage, network, expressed as the owner's limits; no units or stack-specific values are mandated here.
5. availability — the operating periods during which the host is expected to be reachable, expressed with a timezone. Offline periods are recorded as absence of availability, not as guaranteed downtime.
6. movement_window — the window in which moves of hosted workloads may begin and end, with timezone.
7. expiry — the instant after which the offer is no longer valid for new assignments. Assignments active at expiry continue only under their own terms; this interaction is unresolved (see section 7).
8. backup_policy_ref — reference to the owner-accepted backup/restore policy covering hosted workloads on this host.
9. offered_at and last_revised_at — timestamps with timezone.

Required distinction: fields 1–9 above must be present for an offer to be assignable. Any future field, for example cloud account credentials, spend limits, or automatic failover settings, is out of scope and explicitly unresolved.

## 4. Hosting assignment fields

Every assignment records:

1. assignment_id — locally assigned identifier.
2. offer_id — references an existing, valid hardware offer.
3. application and version — the application bundle and reviewed immutable version; add-ons and shared services are listed separately where the deployment bundle requires them (CONCEPT.md dependency awareness).
4. dependencies — databases, background jobs, persistent data, and application-specific requirements that placement must consider.
5. resource_limits — the owner-approved limits drawn from the offer's resources; an assignment must not exceed them.
6. operating_schedule — when the workload may run, with timezone.
7. assignment_expiry — the instant after which the assignment is no longer authorised; renewal requires a new consent check against the current offer.
8. movement_window — inherited from or narrowed against the offer's movement window; moves outside it require re-consent.
9. destination — the approved host identity within this record system; not a network address or cloud endpoint.
10. backup_schedule and backup_policy_ref — scheduled or on-demand backups reference the same verified restore procedure; the backup record itself is separate.
11. retention — how long recovery copies are kept; the data-loss window is acknowledged, not eliminated (TRUST-AND-RECOVERY.md).
12. recovery_custodian — the CEO or appointed officer authorised for recovery material, separate from the manager who created the assignment.
13. proposed_by, proposed_at, consent_confirmed_at, consent_confirmed_by — manager and owner consent timestamps.

Required: assignment_id, offer_id, application, version, resource_limits, assignment_expiry, recovery_custodian, and at least one of operating_schedule or movement_window. All other fields are optional pending separate policy records.

## 5. Consent, withdrawal, and case states

Owner consent is the gate. An owner may revoke future hosting at any time (TRUST-AND-RECOVERY.md hardware boundaries). Revocation does not by itself specify what happens to already running workloads; that handling is unresolved and must be reconciled against application-specific fencing and failure tests (DECISION-GUIDE.md).

Case states:

- valid — offer present, not expired, consent active, resources sufficient, workload within consent scope.
- invalid — missing required field, expired offer, revoked consent, insufficient declared resources, workload outside consent scope, or references a nonexistent offer or backup policy. Invalid assignments must not be deployed.
- withdrawn — owner revoked consent after assignment was valid. No new assignments may reference the offer; in-flight assignments need a separate stop or rollback decision.
- offline — host is not reachable during its declared availability. An offline host cannot make a new backup, and recovery may lose changes since the most recent usable copy (TRUST-AND-RECOVERY.md). Offline is an operational observation, not consent revocation.

Transitions between valid, invalid, withdrawn, and offline are events with timestamps and the actor or observation source. No automatic failover is assumed; automatic failover is a later capability requiring its own evidence (TRUST-AND-RECOVERY.md).

## 6. Synthetic examples

These examples use no real corporation, host, or application data. They demonstrate field shape only.

Example A — trusted host, authentication bundle:
- offer: owner-consented resources for CPU, memory, storage; workload scope limited to authentication and related services; availability expressed with a timezone; movement window aligned to a Sunday maintenance period; backup policy reference with backups every six hours; recovery custodians: CEO and appointed officer.
- assignment: application version and dependencies listed; resource limits within the offer; movement window within the Sunday window; recovery custodian separate from the assigning manager.

This mirrors the illustrative trusted-host example in CONCEPT.md and is not a default.

Example B — volunteer member host:
- offer: limited resource allocation; availability outside the member's working hours with timezone; workload scope restricted to non-sensitive standalone applications; expiry set by the owner; backup policy reference optional pending trusted-storage decision.
- assignment: only if the workload is standalone and within limits; sensitive tokens and authoritative databases are directed to appropriately trusted infrastructure rather than this host (TRUST-AND-RECOVERY.md hardware boundaries).

Example C — invalid:
- offer missing expiry or consent_scope; assignment requesting resources above the offer; workload outside consent scope; expired offer referenced.

Example D — withdrawn:
- valid assignment, then owner revokes consent; assignment state becomes withdrawn; no new writes admitted until a stop or rollback procedure is chosen.

Example E — offline:
- host within declared availability but unreachable; no new backup possible; recovery target prepared separately; automatic failover not assumed.

## 7. Reconciliation needs and unresolved decisions

The following are recorded as open, not resolved:

- What happens to running assignments when an offer expires or is withdrawn (stop, finish, rollback) requires application-specific fencing and failure tests.
- Which workloads are acceptable on volunteer hosts versus trusted infrastructure is undecided (DECISION-GUIDE.md open questions).
- Operating systems, deployment runtime, cloud provider, and spend-limit enforcement are unselected.
- Backup/restore evidence, restore exercises, and measured recovery time and data-loss targets are pending per application.
- Recovery custodian succession and emergency recovery procedures are design decisions, not settled rules.
- Cloud integration is optional and unverified; no provider or cost is assumed.

## 8. Acceptance checks against this specification

Every surfaceable fact traces to the pinned inputs. Checks:

1. Owner consent field present and consent scope distinguished from resources.
2. Invalid, withdrawn, and offline states defined with required handling.
3. Movement window, expiry, timezone, availability, and backup-policy reference present in offer and/or assignment records.
4. No dependency on another task schema; all terms locally defined.
5. Synthetic examples cover valid, invalid, withdrawn, and offline cases.
6. Unresolved decisions are explicitly marked and not implemented.

This document is planning text, not proof that anything works. It must not be treated as accepted until the project owner or an appointed reviewer integrates it against MAP-003 criteria.
