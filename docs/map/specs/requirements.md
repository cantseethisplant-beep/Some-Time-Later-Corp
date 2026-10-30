# Requirements and glossary — MAP-001
Revision: 792b158838aa5214d0156690d24e21e780de542e. Status: proposed specification for review; no app implemented or tested.

## Requirements

| ID | Intended behaviour | Modality | Source path and section | Observable behavioural check |
|---|---|---|---|---|
| REQ-01 | Corporation records administration and recovery contacts/custodians before assignments | required | docs/CONCEPT.md — Proposed journey; docs/TRUST-AND-RECOVERY.md — Proposed roles | CEO and recovery custodian recorded; custodian retrieves only authorised recovery material |
| REQ-02 | Members voluntarily offer hardware/VM/allocation with availability and permitted workloads | required | README.md — The idea; docs/CONCEPT.md — Proposed journey | Offer record lists resources, availability, and acceptable workloads set by owner |
| REQ-03 | CEO or appointed managers choose a reviewed bundle and inspect dependencies/resource requirements | required | docs/CONCEPT.md — Proposed journey | Manager selection recorded with dependency and resource summary |
| REQ-04 | Assignment stays within owner consent and approved limits | required | docs/CONCEPT.md — Proposed journey | Assignment rejected if outside owner offer or limits |
| REQ-05 | Controlled deployment prepared and verified on an approved host before use | proposed | docs/CONCEPT.md — Proposed journey | Deployment verification passes on target host before assignment is active |
| REQ-06 | Authorised users monitor health and request backups or use scheduled backups | required | docs/CONCEPT.md — Proposed journey | Health status visible; every manual or scheduled backup logged |
| REQ-07 | Movement/recovery follows an application-specific procedure recording success or attention items | required | docs/CONCEPT.md — Proposed journey | Movement/recovery log contains outcome and attention items per event |
| REQ-08 | Assignment record: version, dependencies, owner-approved host, limits, schedule, expiry, movement window, backup schedule, destination, retention, recovery custodians. The field list is proposed, not a universal default; fields required by the agreed application policy must be present. Retention and exact times remain undecided. | required | docs/CONCEPT.md — Hosting assignment | All applicable policy-required fields present; missing required fields block assignment creation |
| REQ-09 | Manual and scheduled backups are a requested outcome; using one shared consistent procedure for both is a proposed safeguard. | proposed | docs/CONCEPT.md — Hosting assignment; docs/TRUST-AND-RECOVERY.md — Backup and movement | Manual and scheduled backups each produce a logged result; identical procedure execution is proposed, not verified |
| REQ-10 | Member hardware and optional corporation cloud resources recorded together; no cost/provider/retention targets preset | optional | README.md — The idea; docs/CONCEPT.md — Deployment choices | Cloud account entry possible alongside hardware; no enforced spend limit or provider assumed |
| REQ-11 | Catalogue marks each entry as standalone application, add-on, or shared service | proposed | docs/CONCEPT.md — Dependency awareness | Entry type populated before use in placement |
| REQ-12 | Placement considers databases, background jobs, persistent data, application-specific requirements | proposed | docs/CONCEPT.md — Dependency awareness | Placement validation checks dependency-aware requirements before confirming host |
| REQ-13 | Existing Discord communication functions not rebuilt or merely duplicated | proposed | README.md — What a first version might cover | No feature duplicates existing Discord communication; non-duplicating Discord integration not globally forbidden |
| REQ-14 | Entry is "supported" only after upstream repo/licence, immutable reviewed version, maintenance status, dependencies, permissions, storage model, measured resources, deployment steps, update/rollback procedure, backup/restore evidence | proposed | docs/DECISION-GUIDE.md — Catalogue entry requirements | All catalogue fields populated; a GitHub listing alone does not qualify |
| REQ-15 | Scheduled or clicked backup yields consistent package protected in transit/at rest, integrity verified, completion/failure recorded; keys separate from encrypted copies | proposed | docs/TRUST-AND-RECOVERY.md — Backup and movement | Backup produces verifiable package; result logged; key storage path separate from backup storage |
| REQ-16 | Repeatable rollout to a second corporation: configure a second isolated test corporation without copying the first corporation's private data. Desired outcome with a proposed isolation check, not a completed test. | proposed | — (proposed addition; no source section yet) | Second corporation configured in isolation; first corporation's private data not copied; check proposed, not completed |
| REQ-17 | Hardware owner may withdraw future hosting; withdrawal is recorded and no new assignments are placed on that host. No promise of instant deletion on an offline machine. | proposed | docs/TRUST-AND-RECOVERY.md — Hardware boundaries; Proposed roles | Withdrawal recorded; host excluded from new assignments; offline instant deletion not guaranteed |

## Glossary

- Build Idea 2 — the chosen product: a reusable EVE corporation hosting manager presenting a curated catalogue, recording member hardware and cloud offers, and helping authorised managers assign applications to suitable hosts (docs/CONCEPT.md — Two build ideas).
- Build Idea 1 — fixed corporation software installation; shortlist of Wanderer, Alliance Auth, AA Buyback, Indy Hub, and AA Structures; historical context and possible pilot only, not the product definition (docs/CONCEPT.md — Two build ideas).
- Controller — the platform itself, which needs reliable storage and hosting of its own; existing workloads should keep running during controller outages subject to dependencies (docs/CONCEPT.md — Deployment choices).
- Assignment — a proposed or active placement of an application bundle on an approved host within owner consent and limits (docs/CONCEPT.md — Proposed journey; Hosting assignment).
- Catalogue entry — a reviewed application bundle; "supported" status requires evidence beyond a GitHub listing (docs/DECISION-GUIDE.md — Catalogue entry requirements).
- Hardware owner — a member who offers resources, sets limits, consents to workloads, and may withdraw future hosting; withdrawal does not promise instant deletion on an offline machine (docs/TRUST-AND-RECOVERY.md — Proposed roles; Hardware boundaries).
- Recovery custodian — retrieves or restores specifically authorised recovery material (docs/TRUST-AND-RECOVERY.md — Proposed roles).
- Movement window — the period during which an assignment may be moved between hosts (docs/CONCEPT.md — Hosting assignment).
- Fencing — preventing the previous writer from accepting new writes after a move; never two authoritative writers merely because both hosts appear healthy (docs/TRUST-AND-RECOVERY.md — Backup and movement).
- Hybrid cloud — member resources plus authorised cloud services; cloud costs and account permissions need controls (docs/CONCEPT.md — Deployment choices).

## Proposed safeguards, not independently verified requirements

- Encryption and key separation: backup encryption keys must be managed separately from encrypted copies; deployment authority and permission to decrypt backups should be separate. CEO succession must not silently grant access to every historical secret (docs/TRUST-AND-RECOVERY.md — Backup and movement; Proposed roles).
- Trusted hosts: managers assign only predefined approved workloads within an owner's offer; sensitive tokens and authoritative databases should use appropriately trusted infrastructure (docs/TRUST-AND-RECOVERY.md — Hardware boundaries).
- Hardware boundaries: design should avoid arbitrary remote commands and unrestricted access to the host operating system or personal files. Isolation does not make the physical host owner unable to inspect runtime data (docs/TRUST-AND-RECOVERY.md — Hardware boundaries).
- Fencing and rollback: for a planned move, fence the previous writer before admitting new writes; never allow two authoritative writers merely because both hosts appear healthy; if verification fails, stop and use a tested rollback procedure. Rollback is proposed and not independently verified (docs/TRUST-AND-RECOVERY.md — Backup and movement).
- Offline revocation and availability: a hardware owner may revoke future hosting, but offline revocation cannot guarantee instant workload deletion; an offline host cannot make a new backup, and recovery may lose changes since the most recent usable copy (docs/TRUST-AND-RECOVERY.md — Backup and movement; Hardware boundaries).
- Controller outages: existing workloads should keep running during controller outages subject to their own dependencies; this must be tested, not assumed (docs/CONCEPT.md — Deployment choices).

## Open decisions

- Who operates and pays for the central controller?
- How are CEO identity, delegation, succession, and emergency recovery established?
- Which workloads are acceptable on volunteer hosts, and which need trusted infrastructure?
- Which operating systems, deployment runtime, and cloud provider should the pilot support; how are cloud spending limits enforced, and what happens if costs or capacity exceed the plan?
- What are acceptable recovery time and data-loss targets for each application?
- How does a hardware owner withdraw, including when their machine is already offline?
- Who may read each type of corporation data, and how is consent documented?
- What licensing and distribution model should the eventual product use?
- Discord: do not forbid future useful Discord integration globally; only exclude duplicating existing communication functions.
- No selected stack/providers/retention/recovery targets; Cloudflare was discussed as an optional access and backup component, not a complete deployment manager; provider selection and current feature suitability remain unverified (docs/DECISION-GUIDE.md — Questions still open; docs/TRUST-AND-RECOVERY.md — Backup and movement).
- Retention and exact times for assignment record fields remain undecided.

## Provenance and limits

- Inputs (all four): README.md; docs/CONCEPT.md; docs/DECISION-GUIDE.md; docs/TRUST-AND-RECOVERY.md.
- Source SHA: 792b158838aa5214d0156690d24e21e780de542e.
- Source sections used: README — The idea / What a first version might cover / Project boundaries; CONCEPT — Two build ideas / Proposed journey / Hosting assignment / Deployment choices / Dependency awareness; DECISION-GUIDE — Catalogue entry requirements / Questions still open; TRUST-AND-RECOVERY — Proposed roles / Hardware boundaries / Backup and movement.
- Limits: document checks only, no runtime tests; no app implemented or tested; candidate software names and compatibility are unverified; this is a proposed specification for review, not an accepted requirement set.
