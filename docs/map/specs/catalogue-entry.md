# MAP-005: Catalogue Entry and Evidence Fields

## 1. Purpose and scope

This file specifies what a reviewed application or application-bundle entry must contain in the Eve Cloud build map. It converts the catalogue-entry requirements documented in docs/DECISION-GUIDE.md into a field schema with required/optional distinctions, entry states, evidence conditions, invalidation triggers, and one synthetic unverified example. The schema is derived from the baseline concept inputs — README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md, and docs/TRUST-AND-RECOVERY.md at revision 792b158838aa5214d0156690d24e21e780de542e — without external research or technical verification.

The repository status declares this a concept and planning only artefact: there is no working app, supported deployment, verified software catalogue, or measured hosting cost. Accordingly, this schema is a documentation proposal, not component-tested evidence, not a deployment procedure, and not authority to select a stack. It specifies field shapes and evidence conditions so that, when upstream projects become available, catalogue views can consistently report identity, licence, version, dependencies, permissions, resources, deployment procedures, and backup/restore provenance.

Scope limits stated upfront:
- No upstream candidate has been researched. Names such as Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures and CorpTools appear only as historical planning context from the baseline documents. They are not endorsements, and no upstream identity, licence or version for any of them is stated in this file.
- This is a schema proposal. It is not acceptance of any deployment, not a claim about compatibility, and not a commitment about costs or licences.
- Backup creation and restore verification are treated as distinct evidence items throughout; a backup record never implies a successful restore.
- All open decisions from the baseline are carried forward as unresolved; none are resolved or mandated here.

## 2. Baseline intent vs proposed schema rules

Baseline intent (accepted concept inputs):
- A catalogue entry must record upstream repository and licence, reviewed immutable version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update and rollback procedure, and backup/restore evidence (docs/DECISION-GUIDE.md, "Catalogue entry requirements"). A GitHub listing alone proves none of these.
- A deployment may be a bundle: add-ons and shared services must be distinguished from standalone applications; databases, background jobs and persistent data constrain placement (docs/CONCEPT.md, "Dependency awareness").
- Backup evidence requires a consistent recovery package, integrity verification, separate key management, and a restore exercise; a successful upload is not proof of recoverability (docs/TRUST-AND-RECOVERY.md, "Backup and movement").

Proposed schema rules (new in this file, pending acceptance):
- Required vs optional field classification in sections 4 and 5.
- Four entry states in section 3: candidate, documentation-reviewed, component-tested, supported-for-specific-environment.
- Evidence conditions and invalidation triggers per field group in section 6.
- A synthetic example block in section 7 showing field population without inventing upstream facts.
- Optional fields remain absent until a concrete assignment or policy decision requires them.

Where baseline language says "must" for concept behaviour, that requirement is carried into the schema as an evidence field. Where the baseline leaves a decision open (for example, operating system or cloud provider), the corresponding field is marked unresolved and no default is imposed.

## 3. Entry states

An entry occupies exactly one state. States are progressive but not automatic: evidence for the target state must exist before it is assigned.

| State | Meaning | Minimum evidence |
| --- | --- | --- |
| candidate | Name entered for consideration only. No review performed. | Entry id, proposed upstream name, source of nomination. |
| documentation-reviewed | Upstream documentation inspected and fields populated. | All required identity, licence, version, dependency, permission and resource fields completed from documentation, with source cited. |
| component-tested | At least one deployment-relevant component behaviour observed. | Component test result (install, start, or backup/restore exercise) with date, environment and outcome; failures recorded. |
| supported-for-specific-environment | Entry cleared for assignment in one named environment. | Component-tested plus deployment, rollback and restore evidence specific to that environment; hardware-owner consent and recovery custodian recorded. |

A component-tested result does not imply supported-for-specific-environment. A documentation-reviewed entry is not component-tested. A GitHub listing alone proves none of these states. These distinctions must be visible in every catalogue view.

## 4. Required fields

### 4.1 Identity and provenance

- **entry_id**: stable identifier for this map entry.
- **upstream_name**: name used by the upstream project; `unresolved` if not verified.
- **upstream_repository**: exact upstream repository URL or identifier. Exactness is required; a listing alone proves nothing.
- **upstream_licence**: exact licence identifier from the upstream source. This is distinct from the repository's own reuse licence, which has not been selected (README.md).
- **pinned_version**: reviewed immutable version, with digest or commit where available.
- **version_source**: where the pinned version was observed (release page, tag, digest record).
- **maintenance_status**: upstream maintenance status as observed (active, archived, unknown), with date observed.
- **bundle_role**: one of `standalone-application`, `add-on`, `shared-service`.
- **bundle_members**: for bundles, the identifiers of included applications, add-ons and shared services, and whether each can run independently on a different host.

### 4.2 Dependency and bundle relationships

- **dependencies**: each dependency with name, exact version constraint, relationship type (runtime database, background job, shared service, optional add-on), and whether dependency failure blocks the application.
- **placement_constraints**: databases, persistent data paths, background jobs and application-specific requirements that prevent independent placement.
- **dependency_evidence**: how each dependency relationship was confirmed (documentation, observed deployment, unresolved).

### 4.3 Permissions and trust

- **deployment_authority**: role that may approve deployment (CEO, appointed manager), per the roles table in docs/TRUST-AND-RECOVERY.md.
- **hardware_consent_required**: whether hardware-owner consent is required before assignment.
- **permitted_workloads**: workloads the hardware owner has consented to; workloads excluded.
- **isolation_level**: degree of isolation from the host operating system and personal files. Isolation does not prevent the physical host owner from inspecting runtime data (docs/TRUST-AND-RECOVERY.md).
- **sensitive_data_handling**: which tokens and authoritative databases must use trusted infrastructure rather than volunteer hosts.
- **recovery_custodian**: role authorised to retrieve or restore authorised recovery material; separate from deployment authority.

### 4.4 Resources

- **measured_resources**: CPU, memory, storage and network measurements, with environment, date and method. If not measured, `unmeasured`; estimates are not measured resources.
- **deployment_target**: operating system and deployment runtime. Unresolved pending pilot decision (docs/DECISION-GUIDE.md open questions).
- **cloud_responsibilities**: networking, storage, scheduling and application hosting are separate; provider selection unverified (docs/TRUST-AND-RECOVERY.md).
- **storage_model**: where persistent data lives and how it is identified for backup.

### 4.5 Deployment, update and rollback

- **deployment_steps**: reviewed procedure to prepare and verify a controlled deployment.
- **update_procedure**: how to move to a new pinned version.
- **rollback_procedure**: tested rollback procedure to use if verification fails after update or move.
- **movement_procedure**: for planned moves — destination consent and compatibility, prepare the reviewed version, quiesce writes and jobs, capture or hand over consistent state, verify the destination, change routing, fence the previous writer before admitting new writes. Never allow two authoritative writers merely because both hosts appear healthy (docs/TRUST-AND-RECOVERY.md).
- **controller_outage_behaviour**: whether workloads keep running during controller outages, subject to their own dependencies; this must be tested (docs/CONCEPT.md).

### 4.6 Backup and restore evidence (distinct items)

- **backup_schedule**: scheduled or on-demand backup frequency and trigger.
- **backup_consistency**: method used to produce a consistent recovery package (quiesce, snapshot, application-specific).
- **backup_integrity**: integrity verification performed on the backup copy.
- **backup_keys_managed_separately**: whether encryption keys are stored separately from encrypted copies (required by docs/TRUST-AND-RECOVERY.md).
- **backup_record**: completion or failure recorded for each backup.
- **restore_exercise**: whether a restore has been performed, with date, environment, result and data-loss window observed.
- **restore_verified**: boolean. A successful upload is not proof of recoverability; only a restore exercise counts.
- **acceptable_data_loss_window**: measured or target window; recovery may lose changes since the most recent usable copy (docs/TRUST-AND-RECOVERY.md).

## 5. Optional fields

Optional fields remain absent until a concrete assignment or policy decision requires them. An unresolved policy must not become a mandate in examples.

- **accepted_host_id**: specific volunteered host registered for this assignment (only when an assignment exists).
- **resource_limits**: owner-approved CPU/memory/storage limits for the assignment.
- **operating_schedule**: permitted operating period and movement window.
- **assignment_expiry**: when the assignment expires.
- **backup_schedule_override**: assignment-specific schedule differing from the entry default.
- **movement_window**: window during which a move may occur.
- **cloud_spending_limit**: if cloud resources are used, the enforced limit and breach behaviour (open question in docs/DECISION-GUIDE.md).
- **successor_recovery_access**: CEO succession and emergency recovery access rules; exact rules remain a design decision (docs/TRUST-AND-RECOVERY.md).

## 6. Evidence conditions and invalidation triggers

Each field group carries evidence conditions (when the value is considered valid) and invalidation triggers (when the field reverts to `unresolved` and the entry state is reconsidered). The following groups specify when fields may be deemed valid and when they must revert:

- **upstream identity, licence and version**: invalidated if the upstream repository moves, the licence changes, or the pinned version is superseded without re-review.
- **dependency relationships**: invalidated if a dependency version, database schema or background-job contract changes.
- **deployment, update and rollback**: invalidated by a failed deployment, failed rollback test, or failed controller-outage test.
- **backup and restore**: invalidated if no restore exercise has succeeded within the `acceptable_data_loss_window`, keys are co-located with encrypted copies, or a backup failure is unrecorded. *Note*: the time-window question is tied to the existing `acceptable_data_loss_window` field; no separate retention-period policy is defined.
- **supported-for-specific-environment**: revoked if the environment changes (OS, runtime, host or cloud provider), the host withdraws consent, or measured resources no longer match the host offer.

When any trigger fires, only the affected field group is marked `unresolved`; the rest of the map is not automatically invalidated. Backup creation failure and restore verification failure are separate triggers and must be recorded separately.

## 7. Synthetic unverified example

The entire block below is synthetic and illustrative. It does not describe any real upstream project, and no upstream facts have been invented as fact. Every value marked `[synthetic]` is a placeholder for schema demonstration only and must not be copied into a live catalogue as evidence. No value in this example is a default or factual assertion.

```
entry_id: cat-entry-0001 [synthetic]
state: candidate
upstream_name: example-community-app [synthetic]
upstream_repository: https://example.org/unknown [synthetic placeholder]
upstream_licence: unresolved
pinned_version: unresolved
version_source: none
maintenance_status: unknown
bundle_role: standalone-application [synthetic]
bundle_members: [] [synthetic]
dependencies:
- name: example-database [synthetic]
  version_constraint: unresolved
  relationship_type: runtime-database
  failure_blocks_application: [synthetic]
  dependency_evidence: unresolved
placement_constraints: persistent data at /var/lib/example-app [synthetic]
deployment_authority: unresolved
hardware_consent_required: [synthetic]
permitted_workloads: unresolved
isolation_level: unresolved
sensitive_data_handling: unresolved
recovery_custodian: unresolved
measured_resources: unmeasured
deployment_target: unresolved
cloud_responsibilities: unresolved
storage_model: unresolved
deployment_steps: unresolved
update_procedure: unresolved
rollback_procedure: unresolved
movement_procedure: unresolved
controller_outage_behaviour: unresolved
backup_schedule: unresearched
backup_consistency: unresearched
backup_integrity: unresearched
backup_keys_managed_separately: unresearched
backup_record: none [synthetic]
restore_exercise: none [synthetic]
restore_verified: [synthetic]
acceptable_data_loss_window: unresearched
```

## 8. Unresolved decisions (carried from baseline, not resolved here)

- Who operates and pays for the central controller.
- CEO identity, delegation, succession and emergency recovery establishment.
- Which workloads are acceptable on volunteer hosts and which need trusted infrastructure.
- Operating systems, deployment runtime and cloud provider for the pilot.
- Cloud spending-limit enforcement and over-capacity behaviour.
- Acceptable recovery time and data-loss targets per application.
- Hardware-owner withdrawal procedure, including when the machine is already offline.
- Who may read each type of corporation data and how consent is documented.
- Product licensing and distribution model.

None of these is settled by this schema, and none may be used to justify a stack choice or deployment.

## 9. Acceptance checks for this schema (proposed)

- Every required field has a value, `unresolved`, or an explicit reason for absence.
- Candidate names from the planning discussion appear only as synthetic placeholders, never as verified upstream identities.
- Entry-state transitions require cited evidence; no state is inferred from a name listing.
- Backup fields and restore fields are separate; `restore_verified` is never derived from a backup upload.
- All open decisions in section 8 remain listed and unresolved.
- The synthetic example in section 7 is explicitly labelled illustrative; no value is a default.
- The invalidation trigger for backup-and-restore references the existing `acceptable_data_loss_window` field rather than an undefined retention period.

---
*End of specification.*
