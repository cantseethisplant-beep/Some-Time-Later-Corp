# Application Release and Rollback Lifecycle

## Scope and Intent

This specification defines the intended review, pinning, update and rollback lifecycle for approved application bundles within the Some Time Later Corp hosting platform concept. It is derived from the user-intent baseline documented in revision `792b158838aa5214d0156690d24e21e780de542e` across `README.md`, `docs/CONCEPT.md`, `docs/DECISION-GUIDE.md`, and `docs/TRUST-AND-RECOVERY.md`. No upstream technical verification has been performed; no installation, runtime test, or universal rollback promise is claimed. The scope is bounded to documentation and design decisions visible in the supplied inputs.

The purpose of this document is to separate proposed, reviewed, approved-for-environment, deployed, superseded, and withdrawn releases and to surface dependency changes, data/schema migration prerequisites, backup requirements, and the limits of any rollback procedure. All unresolved questions and open items are preserved as such; no policy decision here should be read as mandate or final position.

## Release Lifecycle Stages

The release lifecycle is defined across six sequential but not necessarily immutable stages. A release may transition between stages under the conditions described below. At any point, the current state of a release must be identifiable in the platform's tracking records.

### Proposed Release

A **proposed release** arises when an appointed manager identifies a reviewed application bundle and proposes an assignment within a hardware owner's consent and limits (CONCEPT.md, "Hosting assignment"). At this stage, the bundle is not yet committed to any host. The proposal includes the application version, dependency list, resource requirements, and intended deployment parameters. No deployment authority has been granted, and no host has been confirmed.

### Reviewed Release

A **reviewed release** occurs when the platform prepares and verifies a controlled deployment on an approved host (CONCEPT.md, "Deployment choices"). This stage involves checking that the bundle's dependencies are compatible with the target host's runtime, that resource limits are respected, and that the deployment steps are well-defined. The review does not constitute approval for production deployment; it confirms that the bundle can be safely attempted on the nominated host. Resolution of any identified compatibility gap returns the bundle to proposed status.

### Approved-for-Environment Release

An **approved-for-environment release** is a reviewed release for which the appointed manager has granted deployment authority for a specific environment (hardware owner's consent, resource limits, operating schedule). This stage records that the release has been validated against the environment's constraints but does not imply the release is currently running. Approval may be granted with conditions (e.g., "backup must be taken before deployment").

### Deployed Release

A **deployed release** is one that is actively running on an approved host. The platform records the host identifier, the bundle's immutable version, the deployment timestamp, and the current health status. A deployed release may have one or more associated backups, recorded with their integrity verification status (TRUST-AND-RECOVERY.md, "Backup and movement").

### Superseded Release

A **superseded release** is a previously deployed release that has been replaced by a newer approved-for-environment release on the same host. The superseded release remains recorded in the platform's history for rollback purposes but is no longer the active deployment. The conditions under which a release becomes superseded (e.g., automatic promotion, manager decision) must be documented per-application.

### Withdrawn Release

A **withdrawn release** is a release that has been intentionally removed from active consideration before or after deployment. A withdrawn release may arise from a manager's decision, a hardware owner's revocation of consent, or the discovery of a critical issue. Withdrawn releases are recorded with the reason for withdrawal and any rollback or migration actions taken.

## Dependency Changes

Application bundles may include the application and its add-ons as a single deployment unit (CONCEPT.md, "Dependency awareness"). The platform's catalogue must distinguish standalone applications from add-ons and shared services. When a dependency changes—such as an updated library, a versioned module, or a database schema migration—the following must be recorded:

- The dependent component's previous and new version identifiers.
- The affected bundle(s) that reference the component.
- The compatibility assessment between the new dependency and the existing deployment.
- Any required data/schema migration steps (see "Data/schema migrations" below).
- The owner of the change and the approval date.

No universal compatibility guarantee is provided. Each application's dependency update procedure is application-specific and must be evidenced separately.

## Data/Schema Migrations

Data or schema migrations may be required when a release introduces changes to persistent state, database structure, or configuration formats. The platform does not implement or validate migration steps; rather, the following are documented for each bundle:

- Whether a migration is required for the release to function.
- The migration procedure as specified by the application's upstream documentation (not independently verified).
- The backup prerequisites before migration execution (see "Backup prerequisites" below).
- The rollback procedure if the migration fails or produces unintended consequences.
- The estimated data-loss window, if any, and the measured restore evidence (TRUST-AND-RECOVERY.md notes that recovery may lose changes since the most recent usable copy).

Migration steps are **not** executed or tested as part of this specification. They are recorded as adapter-specific evidence needed later.

## Backup Prerequisites

Before any release transition that modifies persistent state—especially deployment, migration, or supersession—backup prerequisites must be satisfied. These are derived from TRUST-AND-RECOVERY.md:

- A scheduled or clicked backup must produce a consistent recovery package.
- The backup must protect data in transit and at rest.
- Integrity verification (e.g., checksum or signature) must be recorded upon backup completion.
- A successful upload to storage is not proof of recoverability; a restore exercise is required.
- Backup is not a live standby; an offline host cannot make a new backup.
- Recovery may lose changes since the most recent usable copy.
- Keys must be managed separately from encrypted copies.

For any release transition, the platform must record whether a backup has been taken, its integrity verification result, and the date of the backup. If no backup exists, the transition must be flagged as high-risk, and the user must execute a backup before proceeding.

## Limits of Rollback

Rollback is not a universal promise. The limits of any rollback procedure are application-specific and must be documented on a per-release basis. Key limits, derived from TRUST-AND-RECOVERY.md, include:

- **Planned move**: To move a release to a new host, the following steps are required: verify destination consent and compatibility; prepare the reviewed version; quiesce writes and background jobs; capture or hand over consistent state; verify the destination; change routing; and fence the previous writer before admitting new writes. If verification fails at any step, the rollback procedure documented for the release must be used.
- **Emergency recovery**: Requires a prepared target and accessible recovery data. Automatic failover is a later capability requiring its own evidence; it is not assumed here.
- **Two authoritative writers**: Never allowed merely because both hosts appear healthy. Rollback procedures must ensure that only one host at a time holds authoritative state.
- **Restore limitations**: Recovery may lose changes since the most recent usable copy. No rollback procedure can guarantee restoration of changes made after the last verified backup.
- **No runtime test or universal rollback promise is provided**. Each release's rollback procedure, if one exists, is a later adapter-specific requirement.

If a rollback is necessary, the platform must record the reason for the rollback, the procedure followed, and the outcome. Rollback decisions must not be taken silently; the reason and any residual risk must be communicated.

## Later Adapter-Specific Evidence Needs

The following items are identified as later adapter-specific evidence needs. They are not part of the current scope but must be addressed before the platform can claim a complete release and rollback lifecycle for any application:

- **One complete deployment and recovery demonstration** for at least one application bundle, including a verified backup and a tested restore exercise (DECISION-GUIDE.md, "One complete deployment and recovery demonstration").
- **Upstream repository and licence**, reviewed immutable version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update and rollback procedure, and backup/restore evidence for each catalogue entry (DECISION-GUIDE.md, "Catalogue entry requirements"). None of these are presently verified in this repository.
- **Owner decisions** on CEO identity, delegation, succession, and emergency recovery (DECISION-GUIDE.md, "Questions still open").
- **Workload acceptability** on volunteer hosts versus trusted infrastructure (DECISION-GUIDE.md, "Questions still open").
- **Operating systems, deployment runtime, and cloud provider** support scope (DECISION-GUIDE.md, "Questions still open").
- **Cloud spending limits enforcement** and capacity-exceedance handling (DECISION-GUIDE.md, "Questions still open").
- **Acceptable recovery time and data-loss targets** for each application (DECISION-GUIDE.md, "Questions still open").
- **Hardware owner withdrawal procedure**, including when a machine is already offline (DECISION-GUIDE.md, "Questions still open").
- **Data consent documentation** and read-access policies (DECISION-GUIDE.md, "Questions still open").
- **Licensing and distribution model** for the eventual product (DECISION-GUIDE.md, "Questions still open").

These items must be resolved per-application before the release lifecycle for that application can be considered complete. No item may be assumed or invented from outside the supplied inputs.

## Unresolved Decisions and Open Items

The following decisions remain open and must be resolved by the project owner or an appointed reviewer before this specification can be considered final for any application:

1. Who operates and pays for the central controller? (DECISION-GUIDE.md)
2. How are CEO identity, delegation, succession, and emergency recovery established? (DECISION-GUIDE.md)
3. Which workloads are acceptable on volunteer hosts, and which need trusted infrastructure? (DECISION-GUIDE.md)
4. Which operating systems, deployment runtime, and cloud provider should the pilot support? (DECISION-GUIDE.md)
5. How are cloud spending limits enforced, and what happens if costs or capacity exceed the plan? (DECISION-GUIDE.md)
6. What are the acceptable recovery time and data-loss targets for each application? (DECISION-GUIDE.md)
7. How does a hardware owner withdraw, including when their machine is already offline? (DECISION-GUIDE.md)
8. Who may read each type of corporation data, and how is consent documented? (DECISION-GUIDE.md)
9. What licensing and distribution model should the eventual product use? (DECISION-GUIDE.md)

No policy decision in this document should be read as resolving any of the above items. Each remains a separate condition for future acceptance.

## Verification Checklist

Before a release transition is executed, the following checks should be performed and recorded. This list is derived from the supplied inputs and does not claim completeness:

- [ ] The release's current lifecycle stage is identified and recorded.
- [ ] If the transition involves a dependency change, the compatibility assessment is documented.
- [ ] If the transition involves a data/schema migration, the migration procedure and backup prerequisites are documented.
- [ ] A backup has been taken and its integrity verified, or a flag indicating no backup exists is recorded.
- [ ] The rollback procedure for the release is documented and accessible.
- [ ] The release's target environment (host, resource limits, operating schedule) is confirmed.
- [ ] The hardware owner's consent for the transition is recorded.
- [ ] The appointed manager's approval for the transition is recorded.

Completion of every item on this checklist is not required for all transitions; unresolved items must be flagged and addressed per the "Later adapter-specific evidence needs" section.

