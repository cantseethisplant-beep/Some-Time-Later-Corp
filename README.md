# Current direction: server-AI blueprint handoff v4

Read [the current blueprint guide](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/main/docs/map/WH-BLUEPRINT.md), MAP-052 draft PR #46. The server AIs are the future builders; the laptop has no required build/runtime/recovery role. V4 has twelve focused gap dispositions, portable intake and a dependency-safe proposed server queue. 188 specification checks pass, including 52 contract fixtures; component/runtime evidence and independent acceptance remain open. No server was contacted/launched by this handoff, no app was built and no cloud provisioned. Use read-only server intake and independent review before admitting implementation tasks under existing authority. Preserve public MAP/private BUILD ownership separation, selected-repo/credential boundaries and free-only inference controls. Do not restart the old laptop Hermes loop or copy its Windows secrets/runtime state to the server.

Earlier status/direction sections below are historical when they conflict with v4.

---

# Current direction: WHMapper with Tools and optional Hosting modules

The owner favours two mods to EVE-WHMapper: WH Tools and optional Hosting, with Oracle Always Free investigated as a backend behind Cloudflare. Read docs/map/WH-BLUEPRINT.md and docs/map/research/RESEARCH-HANDOFF.md. Research handoff MAP-049 is completed as draft PR #43; the owner-directed v2 proposal is draft PR #44, authored/reconciled by Codex from native Hermes research. Preserve the distinction between inspected/documented source, proposed defaults, owner requirements and actual runtime evidence. Core IDs follow the pinned mapper; a supported runtime plugin ABI has not been demonstrated, so the proposed integration uses compile-time modules and a maintained bridge. No implementation/deployment, cloud account change, existing-server use, paid purchase, merge or independent acceptance is authorised merely by these planning records. The completed workers are stopped; do not restart an audit loop without a new owner request.

---

# WH blueprint planning package — complete for review

Start with the [WH blueprint guide](docs/map/WH-BLUEPRINT.md). All seven planning stages are published as drafts, including the [corrected consolidated blueprint](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/36). The guide links exact revisions, source evidence, build order, tests and the OD-01..14 decision/evidence register. WH mapping/intel/operations is the core; cloud is optional. Completion means the planning package is assembled, not that the app is implemented, independently accepted or build-ready. No drafts were merged.

---

# Current owner direction: wormhole tool first

Read [docs/map/WH-FIRST-BRIEF.md](/docs/map/WH-FIRST-BRIEF.md). The owner clarified that the app is primarily a WH mapping/intel/operations tool; cloud hosting is an addition. That brief takes precedence over older hosting-first descriptions below for new WH tasks. Study Pathfinder and EVE-WHMapper; exclude RIFT. Existing hosting drafts remain unaccepted optional background. Native Hermes may perform the finite WH draft/audit/repair sequence from pinned supplied sources; no automatic acceptance, merge or app implementation. Preserve all free-only, claim, security and request-budget gates.

---

# Some Time Later Corp

A public production workbench where people and conversational AIs take small, claimed tasks towards a checked, complete map for building **Eve Cloud**.

The goal is to resolve research, choices, dependencies and component checks during map production, so the later build can follow a prepared specification without restarting discovery or repeating broad testing and reconfirmation. Accepted evidence is reused within its recorded versions and conditions. Final integration and deployment still need checks against the actual assembled app.

**Current stage: map production. The map is incomplete; the app has not been built.** Updated: 30 October 2026.

## Start working

1. Read [AI-CONTEXT.md](AI-CONTEXT.md), [the production rules](docs/PRODUCTION.md) and [the map index](docs/map/INDEX.md).
2. Read the live [task board](production/board.json). Only `ready` tasks are available for work.
3. Claim exactly one task using the board's atomic update procedure. Begin only after the claim is successfully saved and verified.
4. Produce the task's small deliverable and its evidence. Submit it for acceptance, then release the claim.

Every ready task must be completable from existing accepted inputs. It must not need a result from another unfinished task. Dependent work stays in the backlog until all its inputs are accepted. A single task has one owner, and one AI worker has at most one active task.

## Contribute with an AI that cannot use GitHub

Follow [Contribute through your talking AI](CONTRIBUTING.md). Your AI fills a [claim-request packet](production/forms/CLAIM-REQUEST.md); you paste it into the [claim issue form](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new?template=task-claim.yml). Return the coordinator's confirmed board claim to your AI before it starts. Then paste its [finished-work packet](production/forms/FINISHED-WORK.md) into the [submission form](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/issues/new?template=finished-work.yml).

Issues are handled by the project owner or an authorised coordinator. Opening a request does not reserve a task, and sending work does not mark it accepted. The issue forms are handled by a coordinator; they do not automatically grant claims. A separate, time-bounded native-Hermes run is tracked below.


Follow the bounded native-Hermes run, submitted drafts and handoffs in [Hermes production progress](production/HERMES-PROGRESS.md). The public board remains authoritative.

## What we are mapping

Eve Cloud is a proposed EVE Online corporation hosting manager: a reviewed catalogue of community software, hardware voluntarily offered by members, CEO-appointed managers, approved hosting assignments, optional cloud resources, and scheduled or on-demand backup and service movement policies.

Build Idea 1 was a fixed corporation software installation. Build Idea 2 is this reusable app concept. Existing Discord functions should reduce overlap; adding Discord integration is not a requirement.

## Community and proposed video series

**Project creator: VelesPhylakos.**

[Proposal for Pyrex — three-part YouTube series](docs/PYREX-YOUTUBE-PROPOSAL.md), provisionally titled **Crashing the EVE Tool Hosting Economy by Lowering the Barrier to Entry**, is available here as a public draft for discussion. It covers the concept and recruitment, development progress, and a coordinated launch video and EVE forum advertisement once the app is completed and verified.

Publishing this draft in the repository does not approve the proposed videos or promotional launch. No collaboration, dates, financial arrangements or publication commitments have been agreed. The draft's competitor-price statement is supplied planning context and has not been verified by this project; substantiate any comparison before using it in promotion.

## Read the concept and decisions

- [Concept and example journey](docs/CONCEPT.md)
- [Choices and unresolved questions](docs/DECISION-GUIDE.md)
- [Roles, hosting and recovery](docs/TRUST-AND-RECOVERY.md)
- [Evidence and current status](docs/EVIDENCE.md)
- [Build-map completion rules](docs/map/INDEX.md)

The public repository holds the map, queue and non-sensitive evidence. The separate private Eve Cloud repository holds internal technical material and future implementation. There is no automatic private-to-public mirroring. Never put credentials, live corporation data, actual device inventories or private operational details here.

Candidate application names are historical options, not verified support claims. This independent concept does not claim affiliation with CCP Games or upstream projects. A reuse licence has not yet been selected.
