# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/13

Automated critic only; independent review pending.


MAP-015 Task Handoff Record

Claim: hermes-laptop-map-015-auto-20261030 | Commit: 0c4cbf3b20982e9bca751c01b5d9a03b20aa4c4c
Inputs used:
- README.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/CONCEPT.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/DECISION-GUIDE.md @ 792b158838aa5214d0156690d24e21e780de542e
- docs/TRUST-AND-RECOVERY.md @ 792b158838aa5214d0156690d24e21e780de542e

Output produced:
- docs/map/specs/release-lifecycle.md

Checks performed:
- Extracted release lifecycle stages (proposed, reviewed, approved-for-environment, deployed, superseded, withdrawn) from CONCEPT.md hosting assignment and deployment choices, and TRUST-AND-RECOVERY.md roles/backup/movement sections.
- Identified dependency change documentation requirements from CONCEPT.md "Dependency awareness" section.
- Identified data/schema migration documentation needs from DECISION-GUIDE.md "Catalogue entry requirements" and backup/migration implications.
- Identified backup prerequisites from TRUST-AND-RECOVERY.md "Backup and movement" section.
- Identified rollback limits from TRUST-AND-RECOVERY.md "Backup and movement", "Emergency recovery", and planned move procedures.
- Identified later adapter-specific evidence needs from DECISION-GUIDE.md "Catalogue entry requirements" and "Questions still open".
- Verified acceptance criteria are addressed: (1) six release states separated, (2) dependency changes, data/schema migrations, backup prerequisites and rollback limits covered, (3) later adapter-specific evidence defined with no universal rollback promise.

Limitations:
- No upstream technical verification performed; inputs are user-intent baseline only.
- No application-specific rollback procedures are implemented; all are documented as later adapter-specific needs.
- Unresolved questions from DECISION-GUIDE.md "Questions still open" are preserved as open items; none are resolved herein.
- No installation, runtime test, or universal rollback promise is claimed or implied.
- All optional/required distinctions and unresolved decisions are preserved as such.

Remaining work:
- Upstream identity/version/licence verification for catalogue entries.
- Owner decisions on CEO identity, delegation, succession, emergency recovery.
- Workload acceptability classification (volunteer vs trusted).
- Operating systems, deployment runtime, and cloud provider scope.
- Cloud spending limits enforcement mechanism.
- Acceptable recovery time and data-loss targets per application.
- Hardware owner withdrawal procedure.
- Data consent documentation and read-access policies.
- Licensing and distribution model for eventual product.
- One complete deployment and recovery demonstration for at least one application.

Review pending: This specification is a draft deliverable for the MAP-015 task. It must be reviewed against the acceptance criteria and the open items listed above before any integration or acceptance decision.



## Automated screening
{
  "task_id": "MAP-015",
  "decision": "submit_draft",
  "summary": "The draft specification for release-lifecycle.md meets all three acceptance criteria: it separates the six required release lifecycle stages (proposed, reviewed, approved-for-environment, deployed, superseded, withdrawn) with clear definitions and provenance from the pinned inputs; it covers dependency changes, data/schema migrations, backup prerequisites, and limits of rollback with proper documentation of unresolved items; and it defines later adapter-specific evidence needs without claiming a universal rollback promise, explicitly stating no installation, runtime test, or universal rollback promise is provided. The draft correctly preserves unresolved decisions as open items, distinguishes baseline intent from proposed schema rules, maintains backup/migration/restore distinctions, addresses offline limitations, and preserves all unknowns. No unsupported facts are claimed, and all examples are clearly marked as illustrative.",
  "findings": []
}
