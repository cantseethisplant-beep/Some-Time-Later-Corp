# Hermes production — resume here

Updated: 30 October 2026, 02:10 UTC.

**RUN RESUMED with user authorisation:** MAP-003 was corrected in the first bounded repair round; Hermes is continuing on MAP-004 using the existing free allowance. The original deadline and request ledger are unchanged. The 15-minute coordinator heartbeat has been restored.

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
- **MAP-004:** backup/recovery task claimed and queued from independent pinned baseline inputs; no dependence on the unaccepted drafts.
- Drafts submitted to independent review: **3**. Accepted real specifications: **0**. Rejected MAP-003 version retained in Git/local archive; its correction is proposed, not accepted.
- Ledger before MAP-004: **13** conservative request attempts including pilot trials and one MAP-003 correction. Ledger and original deadline were not reset. No paid fallback.
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
