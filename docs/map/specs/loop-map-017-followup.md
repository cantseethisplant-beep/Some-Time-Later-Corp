# Consolidated Requirement Proposal — MAP-017 (Loop Follow-up)

**Task:** MAP-017 — Consolidate and clarify requirement modalities and open decisions
**Claim worker:** hermes-laptop-map-017-auto-20261030
**Claim commit:** bfd59c7f841e6db08a8003aee31f6edee5ec1b49
**Loop:** follow-up, cycle 1, area requirements, key gap-key-requirements-001 (loop policy 1)
**Output path:** docs/map/specs/loop-map-017-followup.md
**Status:** unaccepted proposal for review only. Not accepted requirements, not technical evidence, no app implemented or tested.

## 1. Evidence status and classification rules

All four baseline inputs — README.md, docs/CONCEPT.md, docs/DECISION-GUIDE.md and docs/TRUST-AND-RECOVERY.md — are supplied at revision 792b158838aa5214d0156690d24e21e780de542e. Evidence type: user-intent baseline; no upstream technical verification. Requirement statements REQ-01 through REQ-17 are taken from docs/map/specs/requirements.md at revision c6cc2de20805455eb55c0343394d01225ff41ffd (MAP-001 draft), which is explicitly "UNACCEPTED COMPLETED DRAFT FOR REVIEW ONLY; not requirements or technical evidence." Its required/proposed/optional labels are preserved here as consolidation status labels only; they do not make anything accepted.

Status taxonomy:

- **required** — consolidation gate label carried from the MAP-001 draft; not a baseline "must" unless the Modality column says so.
- **proposed** — baseline expresses a suggestion, or the draft marks it proposed/optional and it remains unreviewed.
- **open decision** — a listed question the baseline answers nowhere; used only in Section 3, never for REQ rows.

Modality rule: may/should/must are preserved exactly as the baseline phrases them and are never collapsed. Where the baseline has no explicit modal verb, Modality reads "intent" (descriptive journey or role statement) rather than inventing one. Negative constraints are preserved as written. Genuinely verified evidence: none.

## 2. Unified requirement table (REQ-01 through REQ-17)

| ID | Behaviour (summary) | Status | Modality | Source provenance | Notes |
|----|---------------------|--------|----------|-------------------|-------|
| REQ-01 | Corporation records administration and recovery contacts/custodians before assignments | required | intent — corporation establishes administration and recovery contacts; CEO appoints managers and recovery custodians (baseline states intended behaviour; no explicit must/should/may verb) | docs/CONCEPT.md — Proposed journey, step 1; docs/TRUST-AND-RECOVERY.md — Proposed roles; rev 792b1588... | Draft label required. No owner choice resolved here. |
| REQ-02 | Members voluntarily offer hardware/VM/allocation with availability and permitted workloads | required | may — offering is voluntary ("Members may have spare hardware"); recording availability and permitted workloads once offered is baseline journey intent, not must | README.md — The idea; docs/CONCEPT.md — Proposed journey, step 2; rev 792b1588... | Draft required; volunteering itself remains optional in the baseline. |
| REQ-03 | CEO or appointed managers choose a reviewed bundle and inspect dependencies/resource requirements | required | intent — CEO or appointed managers choose a reviewed bundle and inspect dependencies and resource requirements (baseline journey step 3; no explicit modal verb) | docs/CONCEPT.md — Proposed journey, step 3; rev 792b1588... | Draft required. |
| REQ-04 | Assignment stays within owner consent and approved limits | required | should — managers should only assign predefined approved workloads within an owner's offer (baseline TRUST Hardware boundaries); a hard "must not exceed" gate is proposed-design, not baseline | docs/CONCEPT.md — Proposed journey; docs/TRUST-AND-RECOVERY.md — Hardware boundaries; rev 792b1588... | Baseline "should" preserved; hard gate labelled proposed-design. |
| REQ-05 | Controlled deployment prepared and verified on an approved host before use | proposed | intent — platform prepares and verifies a controlled deployment on an approved host before use (baseline journey step 5; no explicit modal verb); proposed status reflects the unreviewed draft label | docs/CONCEPT.md — Proposed journey, step 5; rev 792b1588... | Draft proposed. |
| REQ-06 | Authorised users monitor health; request backups or use scheduled backups | required | may — authorised users may monitor health, request backups or use scheduled backups (baseline journey step 6 describes intended behaviour; no explicit should for health-status exposure) | docs/CONCEPT.md — Proposed journey, step 6; rev 792b1588... | Draft required; may/should split preserved. |
| REQ-07 | Movement/recovery follows an application-specific procedure recording success or attention items | required | intent — platform follows an application-specific movement/recovery procedure recording what succeeded and what needs attention (baseline journey step 7; no explicit must verb) | docs/CONCEPT.md — Proposed journey, step 7; rev 792b1588... | Draft required. |
| REQ-08 | Assignment record fields: version, dependencies, owner-approved host, limits, schedule, expiry, movement window, backup schedule, destination, retention, recovery custodians | proposed | could/may — baseline: an assignment could describe these fields; field list is proposed, not a universal default; retention and exact times undecided (OD-14) | docs/CONCEPT.md — Hosting assignment; rev 792b1588... | Draft field list marked proposed; retention/exact times tracked as OD-14. |
| REQ-09 | Manual and scheduled backups use one shared consistent procedure | proposed | should — a backup button and a timed backup should use the same verified procedure (baseline); identical procedure execution is not evidenced | docs/CONCEPT.md — Hosting assignment; docs/TRUST-AND-RECOVERY.md — Backup and movement; rev 792b1588... | Draft proposed. |
| REQ-10 | Member hardware and optional corporation cloud resources recorded together; no cost/provider/retention targets preset | proposed | may — cloud account optional; no enforced spend limit, provider or retention assumed | README.md — The idea; docs/CONCEPT.md — Deployment choices; rev 792b1588... | Draft "optional" preserved; mapped to proposed in this taxonomy. |
| REQ-11 | Catalogue marks each entry as standalone application, add-on, or shared service | proposed | must — catalogue must distinguish standalone applications from add-ons and shared services (baseline); entry type populated before use in placement is proposed design | docs/CONCEPT.md — Dependency awareness; rev 792b1588... | Draft proposed; baseline "must" kept separate from review status. |
| REQ-12 | Placement considers databases, background jobs, persistent data, application-specific requirements | proposed | must — placement must consider databases, background jobs, persistent data and application-specific requirements (baseline); placement validation rule is proposed design | docs/CONCEPT.md — Dependency awareness; rev 792b1588... | Draft proposed. |
| REQ-13 | Existing Discord communication functions not rebuilt or merely duplicated | proposed | should not — negative constraint preserved; non-duplicating Discord integration is not globally forbidden | README.md — What a first version might cover; Project boundaries; rev 792b1588... | Draft proposed; exception wording preserved. |
| REQ-14 | Entry "supported" only after upstream repo/licence, immutable reviewed version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update/rollback procedure, backup/restore evidence | proposed | must — all catalogue fields populated before "supported"; a GitHub listing alone proves nothing (baseline condition) | docs/DECISION-GUIDE.md — Catalogue entry requirements; rev 792b1588... | Draft proposed. |
| REQ-15 | Scheduled or clicked backup yields a consistent package protected in transit and at rest, integrity verified, completion/failure recorded; keys separate from encrypted copies | proposed | must — backup must produce a consistent package, protect it in transit and at rest, verify integrity and record completion/failure; keys managed separately from encrypted copies (baseline must); successful upload is not proof of recoverability | docs/TRUST-AND-RECOVERY.md — Backup and movement; docs/CONCEPT.md — Hosting assignment; rev 792b1588... | Draft proposed; upload success is not recoverability evidence. |
| REQ-16 | Repeatable rollout to a second corporation: configure a second isolated test corporation without copying the first corporation's private data; isolation check proposed, not completed | proposed | none claimed — unsourced proposal; no baseline source section or modal verb to preserve | None claimed — unsourced proposal; MAP-001 draft records no source section | Preserved exactly as unsourced. No baseline section cited; no feasibility inferred. |
| REQ-17 | Hardware owner may withdraw future hosting; withdrawal recorded and no new assignments on that host; no instant-deletion promise on an offline machine | proposed | may — owner may withdraw future hosting (baseline TRUST Proposed roles); withdrawal recorded, host excluded from new assignments, no instant deletion on offline machine (MAP-001 draft proposed-design wording) | Baseline: docs/TRUST-AND-RECOVERY.md — Proposed roles; Hardware boundaries; rev 792b1588...; recording/exclusion wording: MAP-001 draft rev c6cc2de... | Split provenance preserved; baseline reference for REQ-17 kept; offline mechanics tracked as OD-07. |

## 3. Open decisions (all unresolved)

The following decisions are enumerated from docs/DECISION-GUIDE.md — "Questions still open" and docs/TRUST-AND-RECOVERY.md. Each is pinned to its source section, marked unresolved, with rationale. No owner choice is resolved by this draft, and no future owner citation is required to complete this drafting task.

| OD ID | Decision | Pinned source section | Status | Rationale |
|-------|----------|----------------------|--------|-----------|
| OD-01 | Who operates and pays for the central controller? | docs/DECISION-GUIDE.md — Questions still open | unresolved | The baseline asks the question and answers it nowhere. |
| OD-02 | How are CEO identity, delegation, succession and emergency recovery established? | docs/DECISION-GUIDE.md — Questions still open; docs/TRUST-AND-RECOVERY.md — Proposed roles ("Exact rules remain a design decision") | unresolved | Baseline states the need; exact rules are a design decision. |
| OD-03 | Which workloads are acceptable on volunteer hosts, and which need trusted infrastructure? | docs/DECISION-GUIDE.md — Questions still open; docs/TRUST-AND-RECOVERY.md — Hardware boundaries | unresolved | Cross-referenced in both inputs; no workload policy exists. |
| OD-04 | Which operating systems, deployment runtime and cloud provider should the pilot support? | docs/DECISION-GUIDE.md — Questions still open | unresolved | No stack or provider is selected; Cloudflare is discussed only as an optional component. |
| OD-05 | How are cloud spending limits enforced, and what happens if costs or capacity exceed the plan? | docs/DECISION-GUIDE.md — Questions still open | unresolved | No enforcement mechanism or breach behaviour is defined. |
| OD-06 | What are the acceptable recovery time and data-loss targets for each application? | docs/DECISION-GUIDE.md — Questions still open | unresolved | Targets must be decided per application before restore acceptability can be judged. |
| OD-07 | How does a hardware owner withdraw, including when their machine is already offline? | docs/DECISION-GUIDE.md — Questions still open; docs/TRUST-AND-RECOVERY.md — Hardware boundaries | unresolved | REQ-17 records withdrawal as recorded and non-instant; mechanics are open. |
| OD-08 | Who may read each type of corporation data, and how is consent documented? | docs/DECISION-GUIDE.md — Questions still open | unresolved | No data-reader policy or consent record exists in the baseline. |
| OD-09 | What licensing and distribution model should the eventual product use? | docs/DECISION-GUIDE.md — Questions still open; README.md — Project boundaries ("No reuse licence has been selected") | unresolved | No reuse licence selected for this material. |
| OD-10 | Exact rules for CEO succession, emergency recovery and delegation; succession must not silently grant access to historical secrets | docs/TRUST-AND-RECOVERY.md — Proposed roles | unresolved | Design decisions left explicit in the baseline. |
| OD-11 | Permission to decrypt backups is separate from deployment authority; who may decrypt is unresolved | docs/TRUST-AND-RECOVERY.md — Proposed roles; Backup and movement | unresolved | Separation is proposed; decryption rules are not set. |
| OD-12 | Cloud networking, storage, scheduling and application hosting are separate responsibilities; Cloudflare optional only; provider selection and feature suitability unverified | docs/TRUST-AND-RECOVERY.md — Backup and movement | unresolved | No provider chosen; optionality is not a mandate. |
| OD-13 | Automatic failover is a later capability requiring its own evidence | docs/TRUST-AND-RECOVERY.md — Backup and movement | unresolved | Failover is not assumed in any requirement. |
| OD-14 | Retention and exact times for assignment record fields remain undecided | docs/CONCEPT.md — Hosting assignment (annotation carried in the MAP-001 draft for REQ-08) | unresolved | The baseline describes the fields without fixing retention or exact times. |

## 4. Distinctions preserved in this draft

- **Baseline intent:** the four user-approved concept documents at revision 792b1588..., the origin of every behaviour in Section 2.
- **Proposed design:** the status taxonomy, modality annotations, open-decision enumeration and any field-list commentary added by MAP-017; not accepted until separately reviewed.
- **Completed unaccepted reference drafts:** MAP-001 through MAP-011 drafts, including docs/map/specs/requirements.md (source of REQ-01..REQ-17), are review material only. They are not accepted requirements, dependency satisfaction or verified technical evidence.
- **Genuinely verified evidence:** none. No runtime tests, restore tests, component tests or integration checks exist in the supplied inputs, and none are claimed here.

## 5. Modality check

may/should/must appear in the Modality column exactly as the baseline phrases them; nothing is collapsed:

- REQ-01, REQ-03, REQ-05, REQ-07: baseline has no explicit modal verb → recorded as "intent", not upgraded to must.
- REQ-02: voluntary offering = may; recording availability/workloads once offered = journey intent, not must.
- REQ-04: baseline should kept as should; the hard "must not exceed" gate is explicitly labelled proposed-design.
- REQ-06: may for users requesting/using backups; no inferred should for health-status exposure.
- REQ-08: baseline could/may kept; no must gate invented while retention/exact times remain open (OD-14).
- REQ-10: optional preserved.
- REQ-13: should not preserved with its non-duplication exception.
- REQ-15: baseline must preserved; successful upload is explicitly not recast as recoverability evidence.
- REQ-16: no baseline modal verb exists; recorded as "none claimed" rather than inventing should.
- REQ-17: may preserved; withdrawal recorded/excluded/no-instant-deletion wording attributed to the MAP-001 draft as proposed design.

Any hard gate beyond the baseline's own verbs is labelled proposed-design, never a baseline mandate.

## 6. Acceptance criteria mapping and checks performed

- Unified requirement table with status column for all 17 entries: Section 2, rows REQ-01..REQ-17, each with Status ∈ {required, proposed}.
- Every open decision unresolved with a pinned source section and rationale: Section 3, OD-01..OD-14; no future owner decision or citation is required to finish this draft.
- Modality preserved without collapsing may/should/must: Section 2 Modality column and Section 5.
- Source provenance for every requirement entry: Section 2 Source provenance column citing file, section and revision; REQ-16 explicitly unsourced; REQ-17 split provenance (baseline vs MAP-001 draft wording).
- No unsupported inferences or invented evidence: every claim carries a source or explicit "none claimed"; REQ-16 has no baseline section cited; REQ-17's recorded/excluded wording is attributed to the MAP-001 draft.
- Baseline intent vs proposed design vs completed unaccepted reference drafts vs verified evidence: Section 4; verified evidence is empty.

Checks performed: inventory of all nine supplied inputs; REQ-01..REQ-17 extracted from the MAP-001 draft and cross-checked against baseline sections; baseline revision confirmed as 792b1588... for the four concept inputs; per-row modality audit against baseline verbs (may/should/must/intent; no collapse); open decisions enumerated from DECISION-GUIDE.md "Questions still open" and TRUST-AND-RECOVERY.md sections, each pinned and unresolved; REQ-16 confirmed unsourced with no baseline section; REQ-17 baseline reference confirmed as TRUST Proposed roles and Hardware boundaries, with MAP-001-draft wording attributed separately; acceptance criteria mapped in Section 6.

## 7. Limitations and review pending

No GitHub, terminal, network or delegation tools are available; board state and file SHAs were not independently verified. MAP-001..MAP-011 drafts are treated as unaccepted review material, not evidence. No technical verification of upstream software, licence, cost, restore or hosting claims has been performed, and none is claimed. This document is a review input only; acceptance rests with the project owner or an appointed reviewer, and nothing is self-accepted.

Remaining work: coordinator/owner review of this draft; up to two document corrections may apply under task policy; acceptance and any merge remain with the project owner or appointed reviewer.

Review pending: yes — the draft is review input only; no submission, claim release or board update has been performed by this worker.
