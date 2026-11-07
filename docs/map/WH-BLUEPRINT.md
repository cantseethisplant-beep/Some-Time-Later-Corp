# WHMapper blueprint v4 — handoff for server AIs

Updated 7 November 2026. Creator: VelesPhylakos. **MAP-052 draft PR #46** is the current server-AI specification candidate. The owner clarified that the server AIs will build later; the laptop is a documentation workspace, with no required build/runtime/recovery role.

## Start here

1. [Server intake and copy/paste prompt](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-10-server-ai-handoff.md).
2. [Gap review, corrections and remaining gates](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-11-gaps-and-dispositions.md).
3. [Finite proposed server queue and ownership rules](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-12-server-work-queue.md).
4. [Scope and contract reading order](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-00-start.md).

V4 supersedes conflicting v3 policy for P0. The build executor, later production origin and independent recovery host are distinct roles; an online laptop is not a dependency. Server identity/tools/credentials/queue are observed there during intake, not guessed from old notes. This document pass did not connect to or launch the server AIs.

## Current documents

| File | Role |
|---|---|
| [00-START.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-00-start.md) | P0 contract or source/fixture record |
| [01-ACCESS-AND-CONSENT.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-01-access-and-consent.md) | P0 contract or source/fixture record |
| [02-TOOLS-CONTRACT.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-02-tools-contract.md) | P0 contract or source/fixture record |
| [03-DATA-AND-TRANSACTIONS.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-03-data-and-transactions.md) | P0 contract or source/fixture record |
| [04-SCAN-AND-FUTURE-SCOPE.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-04-scan-and-future-scope.md) | P0 contract or source/fixture record |
| [05-RECOVERY-AND-MIGRATIONS.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-05-recovery-and-migrations.md) | P0 contract or source/fixture record |
| [06-BUILD-AND-QUALIFICATION.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-06-build-and-qualification.md) | P0 contract or source/fixture record |
| [07-HOSTING-READONLY.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-07-hosting-readonly.md) | P0 contract or source/fixture record |
| [08-REVIEW-AND-SOURCES.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-08-review-and-sources.md) | P0 contract or source/fixture record |
| [09-CONTRACT-SCHEMA.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-09-contract-schema.md) | P0 contract or source/fixture record |
| [10-SERVER-AI-HANDOFF.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-10-server-ai-handoff.md) | Server handoff/gap/queue contract |
| [11-GAPS-AND-DISPOSITIONS.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-11-gaps-and-dispositions.md) | Server handoff/gap/queue contract |
| [12-SERVER-WORK-QUEUE.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/a3698c314fe6487104f60a8ae94d00120e29ed94/docs/map/specs/map-052-12-server-work-queue.md) | Server handoff/gap/queue contract |

## Improvements and limits

Twelve focused gap dispositions cover laptop assumptions, recovery availability, delete/retry journal ordering, complete lock order, permission-event scope, disabled-module retention, revoking former members, canonical digest/virtual-state fixtures, journal export/checkpoint rules, server ownership/resume/evidence and runtime singleton qualification. V3 findings R01..R07 remain traceable.

**188 document/schema/vector checks passed**, including **52 contract fixtures** across **12 definitions** and **4 digest vectors**. Thirteen output files have exact remote readback and an immutable output revision. These are specification checks; required app/component/runtime qualification and independent acceptance remain open. No app build/deployment or fully build-ready claim is made.

P0 remains the pinned WHMapper plus the manual system-note workflow and optional record-only Hosting. Later scan/core writes, advanced Tools and provider execution are explicit future scope. A capability worksheet is proposed to map desired WH features to inspected/tested base reuse and remaining additions, so the first slice is not mistaken for the completed long-term product.

## Next server step

Hand over the intake prompt and package. The server coordinator first verifies hashes and permissions, performs read-only environment intake and independent review, then admits eligible tasks under its existing authority. The eleven SV tasks are PLANNED proposals, not running workers or a live ready queue. No automatic creation of tasks from unfinished results, paid model fallback, quota reset, unrelated server access or blanket audit loop. Future implementation and raw evidence belong in private Eve-Cloud.

No SDK/Docker installation on the laptop is needed for this phase. Actual server tooling/architecture/repository access, resolved dependencies/licences, bridge/runtime evidence, independent review and private operator/live policy/recovery/domain/account configuration remain specifically owned gates in document 11. No native Hermes inference was used; the old local worker stays stopped at 255/800.

## Immutable identity and artifact

- Draft: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/46. Output: `a3698c314fe6487104f60a8ae94d00120e29ed94`.
- [V4 source/package manifest](WH-BLUEPRINT-V4-MANIFEST.json).
- Portable artifact: `WH-BLUEPRINT-V4-SERVER-HANDOFF.zip`, 38 allowlisted files, SHA-256 `9025f69c8f36fd1824c255cd552852f6aac2f022f01e4becdd26378d09967bc8`; available from the creator.
- [Previous v3 guide](WH-BLUEPRINT-V3.md), [v2 guide](WH-BLUEPRINT-V2.md), [v1 guide](WH-BLUEPRINT-V1.md) are historical.
- [Source-qualified research](research/RESEARCH-HANDOFF.md) retains original dates/limits; no cloud account eligibility is invented.

Submission remains distinct from independent acceptance. Public MAP task ownership stays in [the board](../../production/board.json); future private BUILD authority is defined in document 12.
