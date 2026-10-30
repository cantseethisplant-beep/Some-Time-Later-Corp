# Hermes production — completion-based goal

**Latest user instruction:** progress toward a reasonably usable blueprint for a later build, for as long as needed. The fixed 16:41 stop has been removed. queue_completion mode renews operational leases between model calls without resetting the request ledger or free-only budgets. No recurring Codex checks are enabled.

**Current blocker: local GitHub setup is still missing, and the local worker is not running.** START-HERMES.cmd now accepts the restricted token through hidden local input and starts one worker automatically after successful setup. The Codex connector is separate and is not exported to Hermes. Automatic approval review previously blocked opening the setup UI; the user must complete that local authentication step.

Current scope: approved independent MAP-004..MAP-015 drafts, automated criticism, at most two corrections, draft PRs and explicit claim release. Exhausted repairable drafts are preserved/blocked while other independent tasks continue. Access, scope, quota and missing-input problems stop the loop. Unaccepted drafts never become inputs to dependent work. Finishing the eligible queue leads to a review checkpoint, not automatic acceptance or a completed-blueprint claim.

Usable blueprint target: follow [the build-map coverage and completion gate](../docs/map/INDEX.md) and [production acceptance rules](../docs/PRODUCTION.md): consistent requirements/interfaces/roles/data and architecture, exact upstream versions/licences and applicable evidence, resolved hosting/recovery/rollout decisions, an ordered build sequence and acceptance matrix, with no hidden build-blocking unknowns. Later reconciliation, decisions and scoped verification must become explicit tasks rather than invented evidence.

48 guard/lease/start checks passed. Existing inference ledger remains **18**; no request-budget reset. MAP-001..003 are draft PRs #4/#5/#6. MAP-004's corrected native draft and successful automated critique are saved locally; independent review and publication remain pending.

---

## Historical checkpoints (earlier timing and runtime states are superseded)

# Hermes production — local automation handoff

**Current mode:** the user requested a local automatic drafting/critique/correction/submission loop to avoid recurring Codex check-ins. The local coordinator is running on the existing MAP-004 claim; its native critic found two remaining state/example inconsistencies, automatically queued correction round 2, and then returned submit_draft with no remaining findings. The exact corrected result is saved locally; publishing still awaits local authentication. No new claim is made without an atomic public-board update.

**Local GitHub authentication is still required for automatic publication and further claims.** The Codex connector cannot be exported into the background worker. Setup uses a one-day fine-grained token for this public repository only, Contents and Pull requests read/write, stored Windows-encrypted outside Git and never given to models. Automatic approval review rejected launching the setup UI; the user must complete the local setup manually. Until then the coordinator can finish only the already-claimed task, then waits.

Original hard inference stop: **30 October 2026, 16:41:46 UTC / UK GMT**. Original run `eve-blueprint-20261030` and request ledger preserved. Free-only route, 800-run cap, six total task attempts including native criticism, two correction rounds and 100-account-request reserve remain enforced. No 15-minute Codex automation is active.

Validation: **40 local guard/cycle checks passed**, including a simulated claim/draft/claim-release cycle and stale-SHA refusal. Native JSON critique ran against the real MAP-004 draft and produced actionable feedback. Authenticated unattended GitHub publication is **not yet proven**; do not infer it from the process being alive.

For the user's planned review in about five hours, read local `outputs/hermes-production/AUTONOMOUS-HANDOFF.md`, `LOCAL-AUTOMATION.md`, `PROGRESS.md`, `state/auto.json`, native outbox/critic reports, archives, processed PR records and the live [board](board.json). Source tooling is archived privately in Eve Cloud under `operations/hermes-production/`. Drafts remain unaccepted; no merges or implementation occur automatically.

---

## Historical coordinator checkpoint (superseded operational status)

# Hermes production — resume here

**Automatic Codex check-ins disabled by the user to conserve limit.** The 15-minute heartbeat has been deleted. Hermes may finish its current MAP-004 correction locally, then wait; no automatic submission or next-task claim will occur. The existing 40-minute coordinator-absence stop and original hard deadline remain enabled. Resume through explicit manual coordination; do not recreate the heartbeat without a new user request. Older run details below are historical.

Updated: 30 October 2026, 02:19 UTC.

**RUN RESUMED with user authorisation:** MAP-003 was corrected in the first bounded repair round; Hermes is correcting MAP-004 using the existing free allowance; the user confirmed that the run should continue unattended toward the blueprint. The original deadline and request ledger are unchanged. The 15-minute coordinator heartbeat has been restored.

## Fixed run
- Run: `eve-blueprint-20261030`.
- Launched: **30 October 2026, 01:41:46 UTC (UK GMT)**.
- Hard stop: **30 October 2026, 16:41:46 UTC (UK GMT)**. No extension.
- Maximum 800 inference attempts including pilot and failures; preserve at least 100 account free requests. Provider reported 991/1000 remaining at launch; local conservative ledger counted 10 pilot attempts.
- One active claimed task at a time; six HTTP inference attempts per production task, two native iterations and ten minutes per child. Pilot setup was bounded to ten attempts.
- Zero-priced `nvidia/nemotron-3.5-super-vl:free`, verified against the live model list, with no paid fallback.
- Bounded self-correction: up to TWO correction rounds per task, within six total task HTTP attempts and the existing 800-run cap. Exact findings and rejected files are archived; no automatic acceptance. Stops for unrecoverable/exhausted failures, no eligible tasks, quota/reserve, manual stop or coordinator absent for 40 minutes.

## Submitted and active
- **MAP-001:** native Hermes pilot handed back in [draft PR #4](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/4). Exact GitHub content readback verified; claim released. [Native Markdown handoff](handoffs/MAP-001-hermes-20261030.md).
- **MAP-002:** submitted in [draft PR #5](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/5), claim released; [native handoff](handoffs/MAP-002-hermes-20261030.md). One free request; formatting and wording findings listed in the PR.
- **MAP-003:** first native repair addressed the original four findings; [draft PR #6](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/6) updated with exact readback, source/proposal distinction and documented remaining choices. Claim released to independent review. [Corrected handoff and original history](handoffs/MAP-003-hermes-20261030.md).
- **MAP-004:** first native draft completed; coordinator found backup-operation/copy/restore-state ambiguity and routine-backup versus migration/cutover conflation. Exact feedback queued as correction round 1; original packet retained in local archive. Claim remains exclusively with this run; no unfinished output used by other tasks.
- Drafts submitted to independent review: **3**. Accepted real specifications: **0**. Rejected MAP-003 version retained in Git/local archive; its correction is proposed, not accepted.
- Ledger before MAP-004 correction: **14** conservative request attempts including pilot trials, one MAP-003 correction and MAP-004's initial draft. Ledger and original deadline were not reset. No paid fallback.
- Earlier [PR #3](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/3) is a synthetic copy/paste workflow test, not a product specification.

Pilot production/handoff checks passed. This does not accept the specification. In PR #4, REQ-16 is explicitly an unsourced proposed isolation check requiring review. No runtime, compatibility or restore tests have passed in this drafting run.

## How this works
Native Hermes on the creator's Windows laptop uses its installed document-to-action-items skill and receives only public pinned task inputs. It receives no GitHub credentials or execution tools. A Codex heartbeat coordinates GitHub every 15 minutes through the authorised connection: review packets, create draft PRs, release claims, then claim one next eligible independent task. It never merges or self-accepts.

The local supervisor enforces the absolute deadline, monotonic timer, request accounting, free-model route, child timeout and one-job mailbox. The laptop and Codex must remain running, awake and online. Sleep/offline time does not move the deadline.

## Resume / next action
1. Read this tracker and the live [board](board.json), then inspect the linked PR and handoff.
2. Reuse source revisions and evidence; treat every unaccepted PR as a proposal.
3. Review MAP-004's full native packet; submit as a draft when its handoff gate passes, release its claim and choose one next independent ready task. For diagnosed repairable errors, queue exact feedback through the bounded correction procedure.
4. On diagnosed repairable errors, provide exact feedback through the bounded repair command. After two correction rounds, six task attempts, or an unrecoverable issue, checkpoint/block/release and stop.
5. At the original 16:41:46 UTC hard stop, checkpoint and disable the heartbeat. No extension.

The local resume file is `outputs/hermes-production/COORDINATOR.md`, with `PROGRESS.md`, immutable `RUN.json`, runtime `state/run.json`, `outbox/*-HANDOFF.md` and processed-PR records. Create `outputs/hermes-production/state/STOP` to stop the local supervisor. Credentials and raw native diagnostics stay outside Git.

The map remains incomplete. Later work still needs independent review, reconciliation of accepted specifications and targeted verification before the map can be used as an executable build blueprint.

Private tooling archive: runner, dispatcher, guard checks and coordinator instructions are saved in Eve Cloud under `operations/hermes-production/`. No runtime state or keys are archived. The original stop and correction findings remain in Git history. The existing ledger is preserved; it is not reset on resume. MAP-004 through MAP-015 remain subject to their live board state.

Recovery validation: **21 offline guard/repair tests passed**, and the real MAP-003 first repair completed successfully. Prior files, claim/submission history and all request attempts were preserved. Repairs are coordinated feedback loops, not a guarantee that model errors are detected or that specifications are independently accepted.
