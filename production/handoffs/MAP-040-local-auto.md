# Local native Hermes handoff

Draft PR: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/34

Automated critic only; independent review pending.

# Handoff — MAP-040 WH blueprint candidate

- **Task:** MAP-040 — Assemble WH blueprint candidate from completed parts
- **Claim worker:** hermes-laptop-map-040-auto-20261030
- **Claim commit:** e576ac8c2eda82d594cf3b4a6d6f36b4339daaa4
- **Input revision:** 849978908daabe3d2a45f0e758625eedc4bdde30
- **Output path:** docs/map/specs/loop-map-040-wh-design.md
- **Status:** drafted; not submitted, not accepted, not build-ready

## Diagnosed issues and exact corrections

1. **Crosswalk IDs not applied in body (defect 1).** Section 2 declared canonical MAP-040 identifiers (domain WH-040-D / WH-040-API; operations WH-040-API-01..16; security WH-040-SEC01..08), but Section 5 retained source-draft IDs ('WH-D / WH-API', 'WH-API-01..16', 'WH-SEC01..08'). **Correction:** all body references in Sections 5, 6 and 10 now use the canonical scheme: WH-040-D / WH-040-API domain names, WH-040-API-01 ReadMap through WH-040-API-16 TransferOwnership, and WH-040-SEC01..WH-040-SEC08 misuse cases. The crosswalk table still shows each source task's original local IDs alongside the canonical IDs for traceability; it does not claim the drafts already share identifiers.

2. **Missing licensing/provenance register (defect 2).** Section 3 discussed the two MIT root licences informally and Section 9 T07 mentioned MIT headers only. **Correction:** added Section 4, a structured licensing/provenance register covering both pinned sources. Each row maps commit/path to extracted file list, copyright holder (Pathfinder: Mark Friedrich 2017; EVE-WHMapper: pfh59 2023), licence (MIT both), notice-retention obligation, substantial-copy status (none copied in this design; structural/pattern reference only), and explicitly unverified items (transitive dependencies, assets, EVE game data/ESI terms). The register states that notice retention becomes obligatory only if substantial material is copied later, and that no dependency compatibility, vulnerability, or licence-conflict conclusion is drawn.

## Checks actually performed

- ID consistency check: verified every Section 5/6/10 reference to domains, operations and security cases matches the Section 2 canonical crosswalk (WH-040-D / WH-040-API, WH-040-API-01..16, WH-040-SEC01..08).
- Register completeness check: confirmed Section 4 covers both pinned sources with commit, paths, copyright, licence, notice obligation, copy status and unverified items per the scope requirement.
- Example/field check: inherited MAP-037 request/response examples (valid Signature update, E_CONCURRENT_REVISION with current entity, E_CROSS_MAP, negative shipMass rejection) are cited as unexecuted; required fields (mapId, requestId, entityType, entityId, expectedRevision, idempotencyKey, patch), UUID text ID format, tenant scope and error-code definitions preserved; no example mandates unresolved numeric policy.
- Backup/restore distinction verified throughout: B06 covers scripts only; no restore test executed; backup artefact ≠ recovery evidence.
- Confirmed no implementation, test execution, live ESI access, acceptance, merge or deployment is claimed; all requirements, boundaries, milestones and checks labelled proposed or runtime-only.

## Limitations

- No GitHub, terminal or network tools available; the claim could not be verified against the live production board.
- Evidence limited to pinned inspected extracts; no runtime verification, no full licence/dependency/security audit, no ESI validation.
- No target stack decision, no restore-test evidence, no numeric policy values accepted.
- Word-count aim is a drafting guide, not a substantive acceptance gate.

## Remaining work

- Owner/coordinator review of the proposed reuse decision, requirements, boundaries, milestones, contradiction resolutions and licensing/provenance register.
- Owner decisions pending: stack selection, stale threshold, mass buckets, route weights, opt-in defaults, consent expiry, token rotation interval, audit retention, bootstrap authority.
- Missing upstream evidence: transitive dependency and asset licence checks, EVE game-data/ESI terms, runtime handler behavior.
- Submission via the user-mediated finished-work packet route (no GitHub write access); acceptance, integration and frozen revision remain with the project owner.

## Review pending

Coordinator or project owner review of this candidate blueprint before any acceptance or integration decision. No part of this document is accepted or build-ready.


## Automated screening
{
  "task_id": "MAP-040",
  "decision": "submit_draft",
  "summary": "No material defects found; the draft is complete, internally consistent, cites pinned sources with commit/path/line ranges, labels all proposals as unaccepted, preserves missing evidence and owner decisions, keeps cloud optional, includes the explicit ID crosswalk, licensing/provenance register, requirements, boundaries, UI flows, milestone table, test/evidence matrix, contradiction resolutions, and residual blockers, and does not claim implementation, tests executed, or acceptance.",
  "findings": []
}
