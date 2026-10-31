# Blueprint coverage audit — unaccepted draft

This human-readable view is rendered deterministically from the native Hermes JSON audit. It adds no facts or verification. Independent review remains pending.

Blueprint audit MAP-016: 12 of 13 areas gap, 1 blocked; all evidence at user-intent baseline; 11 open decisions unresolved across DECISION-GUIDE.md and TRUST-AND-RECOVERY.md

## Coverage

### requirements: gap
REQ-01 through REQ-17 defined with mixed modalities (required/proposed/open decision). The unaccepted MAP-001 draft lists REQ-16 as a proposed addition without a source section, while REQ-17 is proposed and cites docs/TRUST-AND-RECOVERY.md, Hardware boundaries / Proposed roles. These draft provenance labels are not verified technical evidence. 11 open decisions from DECISION-GUIDE.md and TRUST-AND-RECOVERY.md remain unresolved: who operates and pays for the central controller, CEO identity/delegation/succession/emergency recovery, acceptable volunteer-host workloads, OS/runtime/cloud provider selection, cloud spending-limit enforcement, recovery targets, owner withdrawal while offline, data-reader consent documentation, and product licensing/distribution model. REQ-13 states "Existing Discord communication functions not rebuilt or merely duplicated" with no defined interface contract. Modality preserved (may/should/must) but no runtime tests or component evidence supports any requirement.
References: MAP-001

### roles: gap
Five roles proposed with authority matrix in MAP-002, but three explicit unresolved decisions remain: CEO succession, emergency access, and delegation rules. Separation of deployment authority from decryption backup permission noted but not formalized. Which workloads are acceptable on volunteer hosts versus trusted infrastructure is unresolved. Authority matrix entries populated, but three design decisions explicitly remain per MAP-002 section 6.
References: MAP-002

### catalogue: gap
Entry state machine defined with 4 progressive states (candidate, documentation-reviewed, component-tested, supported-for-specific-environment) in MAP-005, but no catalogue entry achieves beyond candidate status. All baseline open decisions carried forward unresolved. No upstream candidate researched; names (Wanderer, Alliance Auth, AA Buyback, Indy Hub, AA Structures) appear only as historical planning context. The synthetic example in MAP-005 section 7 is explicitly [synthetic] and must not be copied as fact. Required fields have unresolved or placeholder values.
References: MAP-005

### upstream-evidence: gap
Five evidence categories (user intent, proposed design, documentation-reviewed, component-tested, integration-tested) formally defined in MAP-011 with common provenance schema, but no component-tested or integration-tested evidence exists in this map. All evidence at user-intent baseline level. Documentation-reviewed records only flag issues without technical evidence. Component-tested and integration-tested records marked not performed with unresolved status.
References: MAP-011

### data-model: gap
Data model partially emerged from individual spec documents (MAP-003 offer/assignment schema, MAP-005 catalogue entry schema, MAP-006 operation state model) but lacks unification. No common identifier scheme across catalogue entries, hardware offers, and hosting assignments. Field definitions overlap but don't consistently align across specs. No unified version tracking exists.
References: MAP-003, MAP-005, MAP-006

### interfaces: gap
Only one reference to interfaces exists in REQ-13 of MAP-001 (Existing Discord communication functions not rebuilt or merely duplicated). No defined interface contract, no API surface, no operation contract beyond stated intent, and no integration evidence. The concept mentions deployment choices and hosting assignment but does not define interface specifications.
References: MAP-001

### node-security: gap
Permissions spec (MAP-002) distinguishes deployment authority from decryption backup permission but leaves exact rules unresolved. Hardware boundaries note isolation does not prevent physical host owner from inspecting runtime data. Which workloads are acceptable on volunteer hosts versus trusted infrastructure unresolved. Sensitive tokens and authoritative databases should use trusted infrastructure, but which categories are not defined.
References: MAP-002

### controller: gap
Concept states workloads should keep running during controller outages subject to dependencies, but this must be tested; no measured controller-outage test exists. REQ-16 proposes repeatable rollout to second corporation with proposed isolation check, not completed test. No runtime evidence of controller resilience available.
References: MAP-001

### scheduling: gap
MAP-007 defines time semantics with 8 unresolved policy questions: storage convention (UTC/local/both), canonical timezone source and handling of timezone database updates, display-time timezone rule, DST resolution for recurring local windows, missed-schedule policy, maximum tolerated clock skew between hosts, who may create/change schedules, and how backup scheduling interacts with restore-exercise scheduling. No default schedules, retention periods, or timezones invented; all open questions remain.
References: MAP-007

### recovery: gap
MAP-004 defines backup/recovery outcome labels (Requested, Running, Verified copy, Failed) and restore-exercise categories, but no restore exercises performed. Verified copy does not prove recoverability. Recovery custodian access, key separation implementation, retention, and acceptable data-loss targets all unresolved per Section 4. Example B shows failed restore leaving Verified copy intact, demonstrating the separation.
References: MAP-004

### operations: gap
MAP-006 defines 9 lifecycle states (requested through recovery-required) with transitions, but no operation has been executed. Timeout and unknown outcome handling specified but no default timeouts defined. Retry eligibility and idempotency requirements proposed but all policy decisions unresolved. Never infer success from launch principle stated but no operation has demonstrated completion with verified evidence.
References: MAP-006

### costs: gap
No cost information present in any input. Cloud spending-limit enforcement open question in DECISION-GUIDE.md; no provider or cost assumptions. Cloud responsibilities listed as separate unverified category in MAP-005. Zero cost data across all 13 areas.
References: baseline only; no completed task evidence

### build-and-acceptance: blocked
Completion gate requires: all in-scope requirements have implementation steps and acceptance checks; upstream identities/versions/licences and dependencies resolved; interfaces, roles, data, hosting, rollout decisions consistent; required component evidence exists; no build-blocking unknown remains. None of these conditions are met. 12 of 13 areas are gap status with numerous unresolved decisions; no candidate is build-ready. This area is correctly blocked.
References: baseline only; no completed task evidence

## Proposed follow-ups

### gap-key-requirements-001: Consolidate and clarify requirement modalities and open decisions
Area: requirements
Consolidate REQ-01 through REQ-17 as an unaccepted requirement proposal with required/proposed/open distinctions. Preserve REQ-16 as an unsourced proposal and the baseline reference recorded for REQ-17. Enumerate the open decisions from DECISION-GUIDE.md and TRUST-AND-RECOVERY.md, mark them unresolved and link their source sections. Do not resolve an owner choice or require a future owner citation to complete this drafting task. Preserve may/should/must modalities.
Checks:
- Unified requirement table with status column (required/proposed/open decision) for all 17 entries
- Every open decision is recorded as unresolved with a pinned source section and rationale; no future owner decision or citation is required to complete this task.
- Modality preserved for each requirement without collapsing may, should, must
- Source provenance for every requirement entry
- No unsupported inferences or invented evidence

### gap-key-roles-001: Formalize role authority boundaries and resolve explicit unresolved decisions
Area: roles
Finalize the five-role authority matrix from MAP-002 with explicit rules for CEO succession, emergency access, and delegation scope; separate deployment authority from decryption backup permission as a formal policy; document which workloads are acceptable on volunteer hosts versus trusted infrastructure with owner consent basis.
Checks:
- Complete authority matrix with all role/action entries populated
- CEO succession rules explicitly documented (not assumed)
- Emergency access policy with authorized actors and conditions
- Delegation scope rules with explicit bounds
- Workload classification: volunteer-host vs trusted infrastructure with consent basis
- No mandates from unresolved policies in examples

### gap-key-upstream-001: Establish evidence categorization and validation workflow
Area: upstream-evidence
Define a practical workflow for advancing evidence categories from user intent toward component testing; create template records for documentation-reviewed checks with reviewer, date, method, and criteria_checked; establish invalidation trigger patterns that can be operationalized; ensure five categories remain distinct and not collapsed.
Checks:
- Documentation-reviewed template with all required provenance fields populated
- Invalidation trigger patterns documented for each evidence category
- Five evidence categories preserved as distinct (not collapsed)
- Template records show progression path from intent to component-tested
- No unsupported claims about tested capability

### gap-key-data-model-001: Unify data model across catalogue entries, offers, and assignments
Area: data-model
Design a common identifier scheme linking entry_id, offer_id, and assignment_id; define unified version tracking across pinned revisions; map field overlaps across MAP-003, MAP-005, and MAP-006 to identify redundancies and gaps; create cross-reference matrix showing how each field in one schema relates to others.
Checks:
- Common identifier format usable across all three schemas
- Unified version tracking mechanism with revision pinning
- Cross-reference matrix covering all field definitions across MAP-003/MAP-005/MAP-006
- Identified redundancies and gaps in field coverage
- No field definitions contradict across schemas

### gap-key-interfaces-001: Define minimal interface contract from stated intent
Area: interfaces
Extract the interface requirements implied by the concept: assignment proposal and acceptance, backup and restore operations, move/fencing procedures, and recovery custodian access; formalize these as a minimal interface contract without selecting implementation details; document which interface aspects remain unresolved and require later specification.
Checks:
- Minimal interface contract covering: assignment management, backup/restore operations, movement/fencing, recovery access
- Each interface aspect marked as resolved or unresolved with rationale
- No implementation choices (library, protocol, API surface) introduced
- Contract traces to baseline concept inputs, not invented requirements
- Unresolved aspects explicitly listed

## Exact blockers
- Owner decisions required for 11 open decisions across DECISION-GUIDE.md and TRUST-AND-RECOVERY.md (CEO succession, emergency access, delegation rules, volunteer-host workload classification, OS/runtime/cloud provider selection, spending-limit enforcement, recovery targets, owner withdrawal procedure, data-reader consent, licensing, product distribution model)
- No component-tested or integration-tested evidence exists across any area; all evidence at user-intent baseline
- No working app, supported deployment, or measured restore exists in repository
- 12 of 13 areas are gap status; 1 area (build-and-acceptance) is blocked
- Candidate software compatibility unverified; names only as historical planning context
- Catalogue promotion requires new upstream documentation review and owner decisions; the supplied-text automatic worker cannot establish those facts or promote evidence states.
