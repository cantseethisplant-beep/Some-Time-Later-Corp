# Some Time Later Corp

A public production workbench where people and conversational AIs take small, claimed tasks towards a checked, complete map for building **Eve Cloud**.

The goal is to resolve research, choices, dependencies and component checks during map production, so the later build can follow a prepared specification without restarting discovery or repeating broad testing and reconfirmation. Accepted evidence is reused within its recorded versions and conditions. Final integration and deployment still need checks against the actual assembled app.

**Current stage: map production. The map is incomplete; the app has not been built.** Updated: 28 October 2026.

## Start working

1. Read [AI-CONTEXT.md](AI-CONTEXT.md), [the production rules](docs/PRODUCTION.md) and [the map index](docs/map/INDEX.md).
2. Read the live [task board](production/board.json). Only `ready` tasks are available for work.
3. Claim exactly one task using the board's atomic update procedure. Begin only after the claim is successfully saved and verified.
4. Produce the task's small deliverable and its evidence. Submit it for acceptance, then release the claim.

Every ready task must be completable from existing accepted inputs. It must not need a result from another unfinished task. Dependent work stays in the backlog until all its inputs are accepted. A single task has one owner, and one AI worker has at most one active task.

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
