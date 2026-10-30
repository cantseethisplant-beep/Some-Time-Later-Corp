# Hermes production — resume here

Updated: 30 October 2026, 01:45 UTC.

## Fixed run
- Run: `eve-blueprint-20261030`.
- Launched: **30 October 2026, 01:41:46 UTC (UK GMT)**.
- Hard stop: **30 October 2026, 16:41:46 UTC (UK GMT)**. No extension.
- Maximum 800 inference attempts including pilot and failures; preserve at least 100 account free requests. Provider reported 991/1000 remaining at launch; local conservative ledger counted 10 pilot attempts.
- One active claimed task at a time; six HTTP inference attempts per production task, two native iterations and ten minutes per child. Pilot setup was bounded to ten attempts.
- Zero-priced `nvidia/nemotron-3.5-super-vl:free`, verified against the live model list, with no paid fallback.
- Stops earlier for failed work, no eligible ready tasks, quota/reserve limits, manual stop, or coordinator absent for 40 minutes.

## Submitted and active
- **MAP-001:** native Hermes pilot handed back in [draft PR #4](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/4). Exact GitHub content readback verified; claim released. [Native Markdown handoff](handoffs/MAP-001-hermes-20261030.md).
- **MAP-002:** submitted in [draft PR #5](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/5), claim released; [native handoff](handoffs/MAP-002-hermes-20261030.md). One free request; formatting and wording findings listed in the PR.
- **MAP-003:** hosting-offer/assignment task claimed and queued; independent pinned baseline inputs.
- Real specifications submitted: **2**. Accepted real specifications: **0**.
- Earlier [PR #3](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/3) is a synthetic copy/paste workflow test, not a product specification.

Pilot production/handoff checks passed. This does not accept the specification. In PR #4, REQ-16 is explicitly an unsourced proposed isolation check requiring review. No runtime, compatibility or restore tests have passed in this drafting run.

## How this works
Native Hermes on the creator's Windows laptop uses its installed document-to-action-items skill and receives only public pinned task inputs. It receives no GitHub credentials or execution tools. A Codex heartbeat coordinates GitHub every 15 minutes through the authorised connection: review packets, create draft PRs, release claims, then claim one next eligible independent task. It never merges or self-accepts.

The local supervisor enforces the absolute deadline, monotonic timer, request accounting, free-model route, child timeout and one-job mailbox. The laptop and Codex must remain running, awake and online. Sleep/offline time does not move the deadline.

## Resume / next action
1. Read this tracker and the live [board](board.json), then inspect the linked PR and handoff.
2. Reuse source revisions and evidence; treat every unaccepted PR as a proposal.
3. The coordinator should submit MAP-003 if its complete native output passes scope/handoff checks, then release its claim and select the next independent ready task.
4. On failure, checkpoint and release only this run's claim as blocked; stop rather than loop.
5. At the hard stop, checkpoint unfinished work and disable the heartbeat.

The local resume file is `outputs/hermes-production/COORDINATOR.md`, with `PROGRESS.md`, immutable `RUN.json`, runtime `state/run.json`, `outbox/*-HANDOFF.md` and processed-PR records. Create `outputs/hermes-production/state/STOP` to stop the local supervisor. Credentials and raw native diagnostics stay outside Git.

The map remains incomplete. Later work still needs independent review, reconciliation of accepted specifications and targeted verification before the map can be used as an executable build blueprint.

Private tooling archive: runner, dispatcher, guard checks and coordinator instructions are saved in Eve Cloud under `operations/hermes-production/`. No runtime state or keys are archived. Local ledger after MAP-002: 11 attempts including pilot trials.
