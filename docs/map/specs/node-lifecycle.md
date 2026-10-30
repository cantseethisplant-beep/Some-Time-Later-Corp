# Node Enrolment and Withdrawal Lifecycle

## 1. Scope and Purpose

This specification defines the lifecycle states and transitions for a hosting node within the Some Time Later Corp framework (Build Idea 2). It addresses the enrolment (joining) and withdrawal (leaving) of nodes, the consent and revocation requirements of hardware owners, and the distinction between management-access removal and verified workload/data cleanup on offline physical hosts. All definitions and boundaries are derived from the user-intent baseline documents at revision `792b158838aa5214d0156690d24e21e780de542e` (README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, docs/TRUST-AND-RECOVERY.md). No upstream technical verification, software licences, tests, implementation details, costs, or chosen stack are claimed or invented.

## 2. Lifecycle States and Meanings

The following eight states define the meaningful condition of a hosting node. Each state carries a distinct operational and consent meaning; modality and uncertainty are preserved where the source documents use "may," "should," or "must."

| State | Meaning | Source |
| --- | --- | --- |
| **offered** | The hardware owner has made resources available through the platform, specifying availability, resource limits, and acceptable workload types. No enrolment has been initiated. The node is visible to authorised managers as a potential host but requires explicit consent before any assignment. | docs/TRUST-AND-RECOVERY.md: "Hardware owner offers resources, set limits, consent to workloads and revokes future hosting"; docs/CONCEPT.md: "Members offer a computer, virtual machine or limited resource allocation. They specify availability and acceptable workloads." |
| **enrolment-pending** | A manager has proposed an assignment within the hardware owner's consent limits, and the node is awaiting formal acceptance or decline. The hardware owner's consent conditions have been communicated but the assignment is not yet approved. | docs/DECISION-GUIDE.md: "A manager proposes an assignment within the hardware owner's consent and limits"; docs/CONCEPT.md: Step 4 "A manager proposes an assignment within the hardware owner's consent and limits." |
| **approved** | The hardware owner has explicitly consented to the proposed assignment, and the node is authorised to proceed to the active state. Consent is recorded with provenance (assignment ID, resource limits, operating schedule, expiry). | docs/TRUST-AND-RECOVERY.md: "Hardware owner offers resources, set limits, consent to workloads and revokes future hosting"; docs/CONCEPT.md: Step 5 "The platform prepares and verifies a controlled deployment on an approved host." |
| **active** | The node is running the assigned application bundle within the approved resource limits, operating schedule, and any movement window. The hardware owner has ongoing consent; the platform and authorised users monitor health. | docs/CONCEPT.md: Step 6 "Authorised users monitor health, request backups or use scheduled backups." |
| **disconnected** | The node has lost connectivity or has been deliberately taken offline, but management access remains available if the hardware owner consents. The application workload may be paused or shifted depending on the disconnection cause. This state does **not** imply that workload/data cleanup has been performed; it only indicates the network link is absent. | Inferred from docs/CONCEPT.md Step 7 ("If hosting changes, the platform follows an application-specific movement or recovery procedure") and docs/TRUST-AND-RECOVERY.md: "An offline host cannot make a new backup. Recovery may lose changes since the most recent usable copy." |
| **draining** | The node is being prepared for transition or revocation. Active workloads are quiesced or migrated per application-specific procedures; management access may remain temporarily for coordination, but no new workloads are accepted. Draining is a preparatory state, not a decommissioned state. | docs/DECISION-GUIDE.md: "Quiesce writes and jobs; capture or hand over consistent state"; docs/TRUST-AND-RECOVERY.md: "For a planned move: verify destination consent and compatibility; prepare the reviewed version; quiesce writes and jobs." |
| **revoked** | The hardware owner has withdrawn consent for continued hosting. The platform must cease assignment-related activity. This state distinguishes the *removal of management access* from *verified workload/data cleanup*: revocation removes authorisation, but the physical host may remain in situ until ownership transfer, recycling, or other disposition occurs. Verified workload and data cleanup is a separate process that must be performed after revocation if the hardware owner or platform intends to repurpose or dispose of the host. The hardware owner retains the right to inspect runtime data; the platform does not claim isolation from the hardware owner. | docs/TRUST-AND-RECOVERY.md: "Hardware owner offers resources, set limits, consent to workloads and revokes future hosting"; docs/TRUST-AND-RECOVERY.md: "Isolation does not make the physical host owner unable to inspect runtime data. Sensitive tokens and authoritative databases should therefore use appropriately trusted infrastructure."; docs/DECISION-GUIDE.md: "Volunteer hardware: Uses offered resources — Availability, trust and withdrawal risk — Owner consent, limits and measured uptime." |
| **retired** | The node has been permanently decommissioned. All applicable workloads have been migrated or cleaned up, verified backups have been captured, and the platform no longer tracks the node. Retirement is recorded with a final state transition date and, where applicable, a restoration point. | docs/CONCEPT.md: "Scheduled and manual backups with a tested restore"; docs/TRUST-AND-RECOVERY.md: "A successful upload is not proof of recoverability; a restore exercise is required." |

## 3. Enrolment Process

1. **Resource offer**: The hardware owner registers resources (physical computer, virtual machine, or limited allocation) through the platform, specifying availability, resource limits (CPU, memory, storage), acceptable workload types, operating schedule, and any movement windows. This creates the **offered** state. (CONCEPT.md: "Members offer a computer, virtual machine or limited resource allocation. They specify availability and acceptable workloads.")

2. **Assignment proposal**: An authorised manager selects a reviewed application bundle and proposes an assignment within the hardware owner's consent limits. The proposal includes application version, dependencies, resource limits, operating schedule, assignment expiry, movement window, backup schedule, destination (if moving), retention, and recovery custodians. The node transitions to **enrolment-pending**. (CONCEPT.md: Step 4; DECISION-GUIDE.md catalogue entry requirements.)

3. **Consent and approval**: The hardware owner reviews the proposal and provides explicit consent. If consent is granted, the node transitions to **approved**. If consent is withheld, the node reverts to **offered** and the proposal is rejected. Consent is recorded with provenance. (TRUST-AND-RECOVERY.md: "Hardware owner ... consent to workloads and revokes future hosting.")

4. **Deployment preparation**: The platform prepares and verifies a controlled deployment on the approved host. This includes verifying the reviewed immutable version of the application, its dependencies, permissions, storage model, and measured resources. The node transitions to **active**. (CONCEPT.md: Step 5; DECISION-GUIDE.md: "Before calling an application supported, record its upstream repository and licence, reviewed immutable version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update and rollback procedure, and backup/restore evidence.")

5. **Monitoring and backups**: Authorised users monitor health, request backups or use scheduled backups. Backup procedures must produce a consistent recovery package, protect it in transit and at rest, verify integrity, and record completion or failure. Keys must be managed separately from encrypted copies. (CONCEPT.md: Step 6; TRUST-AND-RECOVERY.md: "A scheduled or clicked backup must produce a consistent recovery package, protect it in transit and at rest, verify integrity, and record completion or failure.")

## 4. Withdrawal and Revocation Process

1. **Consent withdrawal**: The hardware owner withdraws consent for continued hosting. The node transitions from its current state (typically **active** or **draining**) to **revoked**. The platform must cease assignment-related activity for this node.

2. **Distinction: management-access removal vs. verified workload/data cleanup** – This is a critical boundary. Revocation *removes management access authorisation*; it does **not** automatically perform verified workload or data cleanup on the offline physical host. The hardware owner retains the right to inspect runtime data and may remain in possession of the host. Verified workload and data cleanup is a separate, post-revocation process that must be explicitly initiated and evidenced if the hardware owner or platform intends to repurpose or dispose of the host. The platform does not claim isolation from the hardware owner at any point. (TRUST-AND-RECOVERY.md: "Isolation does not make the physical host owner unable to inspect runtime data."; DECISION-GUIDE.md: "Volunteer hardware: ... Withdrawal risk — Owner consent, limits and measured uptime.")

3. **Post-revocation actions** (optional, hardware-owner-dependent):
   - The hardware owner may choose to perform a verified backup before host disposition.
   - The platform may record a restoration point if the hardware owner authorises backup creation.
   - Workload and data cleanup (erasure, migration, or transfer) occurs only with hardware owner consent and evidence.
   - If the host is already offline at the time of revocation, the platform notes the disconnection date and retains the **disconnected** state until the hardware owner or platform initiates verified cleanup.

4. **Retirement**: After verified workload and data cleanup (or after a hardware-owned disposition), the node transitions to **retired**. Retirement is recorded with a final state transition date and, where applicable, a restoration point. If cleanup has not been performed, retirement is recorded with the unresolved cleanup status noted.

## 5. Trust Evidence and Unresolved Identity/Key Mechanism

The following trust evidence is required before a node may transition from **offered** to **approved**:

- **Hardware owner consent**: Explicit, recorded consent to the specific assignment, including resource limits, acceptable workload types, operating schedule, and any movement window. (TRUST-AND-RECOVERY.md.)
- **Application reviewed immutable version**: Upstream repository and licence, reviewed immutable version, maintenance status. (DECISION-GUIDE.md catalogue entry requirements.)
- **Measured resources**: Resource offer must be measured and recorded; no over-subscription beyond the hardware owner's stated limits. (CONCEPT.md; DECISION-GUIDE.md.)
- **Backup/restore evidence**: A tested restore exercise must exist for the assigned application bundle; a successful backup upload is not proof of recoverability. (TRUST-AND-RECOVERY.md.)

**Unresolved decisions** (these must not become mandates in examples or assumed implementations):

- **Identity and key mechanism**: The source documents do not specify a concrete identity or key management mechanism for node enrolment. Potential approaches (certificates, shared secrets, platform-managed keys) are left unspecified. Any implementation must not claim upstream verification or standardisation.
- **Hardware owner withdrawal when machine is already offline**: The documents note this as an open question ("How does a hardware owner withdraw, including when their machine is already offline?"). The specification records the **disconnected** and **revoked** states but does not prescribe the exact procedural steps for offline withdrawal.
- **Recovery custodian separation from deployment authority**: The documents state that "Deployment authority and permission to decrypt backups should be separate," but exact rules remain a design decision. This specification records the requirement as unresolved.
- **Operating systems, deployment runtime, and cloud provider scope**: These are listed as open questions in DECISION-GUIDE.md and are not resolved herein.

## 6. Management-Access Removal vs. Verified Workload/Data Cleanup on an Offline Physical Host

This section explicitly separates two operations that are frequently conflated.

| Operation | When it occurs | What it entails | Platform claim |
| --- | --- | --- | --- |
| **Removal of management access** | Immediately upon revocation consent withdrawal. | The platform revokes its authorisation to manage the node; any existing remote session or agent is terminated per the platform's session revocation procedure. The hardware owner may continue to have local access. | The platform does not claim isolation from the hardware owner. Management-access removal is an authorisation withdrawal, not a technical lockout of the physical host. |
| **Verified workload/data cleanup** | After revocation, optionally after hardware owner consent or host disposition. | The platform or hardware owner performs a verifiable action (backup, erasure, migration, transfer) on the host's workloads and data. This requires physical or remote access, integrity verification, and a documented restore/exercise if recovery is claimed. | The platform does not claim isolation from the hardware owner. Cleanup is a separate process that must be evidenced and cannot be presumed by revocation alone. An offline host cannot make a new backup; recovery may lose changes since the most recent usable copy. |

**Key principle**: Revocation of consent (transition to **revoked**) removes the platform's authorisation. It does not substitute for, and must be explicitly distinguished from, any verified workload or data cleanup on the physical host. The hardware owner retains the right to inspect runtime data and may perform, permit, or decline any cleanup operation.

## 7. Acceptance Conditions and Unresolved Items

This specification is accepted as a draft production document subject to the following conditions:

- All eight lifecycle states are defined with clear meanings derived from the user-intent baseline.
- The distinction between management-access removal and verified workload/data cleanup is explicitly preserved.
- Unresolved decisions (identity/key mechanism, offline withdrawal procedure, recovery custodian separation, OS/runtime/cloud scope) are recorded as open and must not be claimed as settled.
- No upstream technical verification, software licence, test, implementation detail, cost, or chosen stack is claimed or invented.
- Trust evidence requirements are identified; actual evidence collection and verification remain for later integration steps.

**Remaining work and review pending**:

- Resolution of the unresolved identity/key mechanism (must not be invented or assumed).
- Procedure for hardware owner withdrawal when the machine is already offline (open question per DECISION-GUIDE.md).
- Concrete backup/restore evidence requirements for each supported application bundle.
- Definition of recovery custodian separation from deployment authority (rules remain a design decision).
- Validation against any future accepted inputs that may modify these definitions.

## 8. Source Provenance

All definitions, state meanings, and boundaries in this specification trace to the following pinned inputs at revision `792b158838aa5214d0156690d24e21e780de542e`:

- **README.md**: Project concept, status, boundaries.
- **docs/CONCEPT.md**: Two build ideas, proposed journey, hosting assignment, deployment choices, dependency awareness.
- **docs/DECISION-GUIDE.md**: Choice matrix, catalogue entry requirements, open questions.
- **docs/TRUST-AND-RECOVERY.md**: Proposed roles, hardware boundaries, backup and movement, recovery custodian.

No other sources have been used. No upstream technical verification, software licences, tests, implementation, costs, or chosen stack have been invented or claimed.

