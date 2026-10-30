# Permissions and Authority Boundaries — MAP-002

Status: proposed build-map specification; concept baseline only. No working app, deployment, tested restore, measured cost, or selected stack exists.

Source inputs at revision 792b158838aa5214d0156690d24e21e780de542e: README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md. Evidence type: user-intent baseline; no upstream technical verification.

## 1. Purpose and scope

This specification defines the proposed role/action matrix for the Some Time Later Corp hosting manager (Build Idea 2: reusable corporation hosting manager). It is produced from the existing trust and concept baseline only. It describes intended behaviour, not available features. It does not implement the application, choose a deployment runtime or cloud provider, set costs, select a licence, or grant any real-world access.

## 2. Roles and proposed authority

Five roles are covered:

| Role | Proposed authority | Source |
| CEO | Appoint managers and recovery custodians; approve critical policy. | TRUST-AND-RECOVERY.md, "Proposed roles" |
| Appointed manager | Manage explicitly delegated applications and assignments only. | TRUST-AND-RECOVERY.md, "Proposed roles" |
| Hardware owner | Offer resources; set limits; consent to workloads; revoke future hosting. | TRUST-AND-RECOVERY.md, "Proposed roles"; CONCEPT.md, "Proposed journey" |
| Member | Use applications to which they are granted access. | TRUST-AND-RECOVERY.md, "Proposed roles" |
| Recovery custodian | Retrieve or restore specifically authorised recovery material. | TRUST-AND-RECOVERY.md, "Proposed roles" |

Separation of duties: deployment authority and permission to decrypt backups should be separate. CEO succession must not silently grant access to every historical secret. Exact rules for succession, emergency access, and delegation remain design decisions (see section 6).

## 3. Role/action matrix

The matrix distinguishes seven actions: deploy, revoke, move, request backup, retrieve encrypted copy, decrypt, and restore. Two auxiliary actions (set owner limits/consent, grant member application access) are included for context.

| Action | Proposed actor(s) | Required consent / condition | Boundary or limit | Source |
| Deploy | CEO; appointed manager within explicit delegation | Hardware owner consent and limits; predefined approved workloads only | No arbitrary remote commands; no unrestricted access to host OS or personal files | CONCEPT.md, "Proposed journey" steps 3–5; TRUST-AND-RECOVERY.md, "Hardware boundaries" |
| Revoke | Hardware owner revokes future hosting of its offered resources | Owner's own offer; withdrawal mechanics when the machine is already offline are unresolved | Revocation affects future hosting; does not by itself undo an in-flight assignment | TRUST-AND-RECOVERY.md, "Proposed roles"; DECISION-GUIDE.md, open questions |
| Move | CEO or appointed manager per the assignment | Destination consent and compatibility; reviewed version prepared | Planned move: verify destination consent and compatibility; prepare reviewed version; quiesce writes and jobs; capture or hand over consistent state; verify destination; change routing; fence the previous writer before admitting new writes; on verification failure, stop and use a tested rollback; never allow two authoritative writers merely because both hosts appear healthy | TRUST-AND-RECOVERY.md, "Backup and movement"; CONCEPT.md, "Hosting assignment" |
| Request backup | Authorised user per assignment; scheduled or on-demand button | Same verified procedure for a clicked backup and a timed backup | Package must be consistent, protected in transit and at rest, integrity-verified, and completion or failure recorded; a successful upload is not proof of recoverability | CONCEPT.md, "Hosting assignment"; TRUST-AND-RECOVERY.md, "Backup and movement" |
| Retrieve encrypted copy | Recovery custodian (CEO or designated recovery custodian) | Specifically authorised recovery material only | Access limited to material the custodian is authorised to retrieve | TRUST-AND-RECOVERY.md, "Proposed roles" |
| Decrypt | Not assigned in baseline | Permission to decrypt backups is separate from deployment authority | Who may decrypt and under what rules is unresolved | TRUST-AND-RECOVERY.md, "Proposed roles" |
| Restore | Recovery custodian on a prepared target | Accessible recovery data; restore exercise required to prove recoverability | Offline host cannot make a new backup; recovery may lose changes since the most recent usable copy; backup is not a live standby; automatic failover is a later capability | TRUST-AND-RECOVERY.md, "Backup and movement" |

Member baseline action — use granted applications — is recorded in the roles table above and is not repeated as a matrix row.

## 4. Authority boundaries

- Hardware boundaries: managers assign only predefined approved workloads within an owner's offer. Isolation does not prevent the physical host owner from inspecting runtime data, so sensitive tokens and authoritative databases should use appropriately trusted infrastructure. Which workloads are acceptable on volunteer hosts versus trusted infrastructure is unresolved.
- Deployment modes: single host, member distributed, hybrid cloud. Member-distributed operation adds capacity but more trust boundaries and variable availability. The controller needs reliable storage and hosting of its own; existing workloads should keep running during controller outages subject to their own dependencies, and this must be tested.
- Cloud: Cloudflare was discussed as an optional access and backup component, not a complete deployment manager. Provider selection and current feature suitability remain unverified. Cloud networking, storage, scheduling, and application hosting are separate responsibilities.
- Backup is not a live standby. An offline host cannot make a new backup. Recovery may lose changes since the most recent usable copy.

## 5. What this specification does not decide

Consistent with the baseline, this specification does not decide: who operates and pays for the central controller; how CEO identity is established; which operating systems, deployment runtime, or cloud provider the pilot supports; how cloud spending limits are enforced; acceptable recovery time and data-loss targets per application; how a hardware owner withdraws while offline; who may read each type of corporation data and how consent is documented; or the eventual product's licensing and distribution model.

## 6. Unresolved decisions (explicit)

1. CEO succession — exact rules are a design decision. Succession must not silently grant access to every historical secret.
2. Emergency access — a prepared target and accessible recovery data are required; who may access recovery material in an emergency and under what conditions is unresolved. Automatic failover is a later capability requiring its own evidence.
3. Delegation rules — the CEO appoints managers and recovery custodians; the scope of delegated applications and assignments must be explicit; exact delegation rules remain a design decision.

These three items are recorded explicitly because the acceptance criteria for MAP-002 require them to remain visible rather than assumed resolved.

## 7. Modality and evidence note

Modal verbs in this document ("should," "may," "must") reflect proposed intent from the baseline documents, not implemented behaviour. No acceptance checks, component tests, restore tests, or integration tests exist for these permissions yet. This document is an input to later build-map work, not authority to deploy, grant access, or incur costs.

