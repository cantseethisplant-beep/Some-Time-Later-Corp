# Hermes production — resume here

Updated: 30 October 2026, 01:59 UTC.

**RUN STOPPED EARLY at 01:58 UTC:** MAP-003 failed the internal consistency/provenance gate. Supervisor exit verified; heartbeat deleted. No further inference or new task claims.

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
- **MAP-003 — BLOCKED:** unedited native draft preserved in [draft PR #6](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/6). Required backup-policy fields contradict an optional example; withdrawal handling is both unresolved and mandated in an example; proposed schema rules need separate provenance; backup and restore procedures are conflated. [Coordinator findings and native handoff](handoffs/MAP-003-hermes-20261030.md). Claim explicitly released.
- Drafts submitted to normal review: **2**. Additional failed-gate draft preserved for correction: **1**. Accepted real specifications: **0**.
- Stopped ledger: **12** conservative request attempts, including pilot trials. MAP-002 and MAP-003 used one new attempt each. No paid fallback.
- Earlier [PR #3](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/3) is a synthetic copy/paste workflow test, not a product specification.

Pilot production/handoff checks passed. This does not accept the specification. In PR #4, REQ-16 is explicitly an unsourced proposed isolation check requiring review. No runtime, compatibility or restore tests have passed in this drafting run.

## How this works
Native Hermes on the creator's Windows laptop uses its installed document-to-action-items skill and receives only public pinned task inputs. It receives no GitHub credentials or execution tools. During the run a Codex heartbeat coordinated GitHub every 15 minutes through the authorised connection: review packets, create draft PRs, release claims, then claim one next eligible independent task. It never merges or self-accepts.

The local supervisor enforces the absolute deadline, monotonic timer, request accounting, free-model route, child timeout and one-job mailbox. The laptop and Codex must remain running, awake and online. Sleep/offline time does not move the deadline.

## Resume / next action
1. Read this tracker and the live [board](board.json), then inspect the linked PR and handoff.
2. Reuse source revisions and evidence; treat every unaccepted PR as a proposal.
3. Correct MAP-003's required-field/example contradiction, source/proposal distinction and withdrawal/backup semantics before resubmission. The preserved PR is a correction reference, not an accepted input. No next task was claimed.
4. On failure, checkpoint and release only this run's claim as blocked; stop rather than loop.
5. The run is already stopped and its heartbeat deleted under the quality-failure rule. The original deadline remains unchanged; no automatic restart or extension.

The local resume file is `outputs/hermes-production/COORDINATOR.md`, with `PROGRESS.md`, immutable `RUN.json`, runtime `state/run.json`, `outbox/*-HANDOFF.md` and processed-PR records. Create `outputs/hermes-production/state/STOP` to stop the local supervisor. Credentials and raw native diagnostics stay outside Git.

The map remains incomplete. Later work still needs independent review, reconciliation of accepted specifications and targeted verification before the map can be used as an executable build blueprint.

Private tooling archive: runner, dispatcher, guard checks and coordinator instructions are saved in Eve Cloud under `operations/hermes-production/`. No runtime state or keys are archived. Final local ledger: 12 attempts including pilot trials. MAP-004 through MAP-015 remain available subject to their live board state; no new claims were taken by this run.
