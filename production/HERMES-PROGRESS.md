# Hermes blueprint production — resume here

Updated: 30 October 2026.

## Goal and current stage

Produce a checked, consistent build blueprint for Eve Cloud through the public task board. The blueprint is incomplete and the app is not built. Work is submitted for review before it can become accepted map evidence.

## Current run

- Laptop runtime: installed native Hermes Agent.
- Inference route: OpenRouter `openrouter/free`; paid fallback disabled in this worker.
- Selected skill: installed `document-to-action-items`, applied to pinned public text.
- Pilot task: **MAP-001 — requirements and glossary**.
- Claim worker: `hermes-laptop-map001-20261030`.
- [Saved pilot claim](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/f128e33da514b30d0de0084932df25a12187119d/production/board.json).
- Pilot: running; no accepted output or PR yet.
- The first budget-wrapper attempt failed during streaming; it was preserved, corrected and retried under the same claim/cumulative counter.
- The 15-hour production window is authorised **only after the one-task pilot passes and reaches review**. Its exact start/deadline will be recorded here on launch.

## Limits

Maximum 15 hours from launch, 800 model-request attempts including the pilot and retries, a 100-request account reserve, one active Hermes claim at a time, six attempts per task, ten minutes per child. Stop earlier on a blocked worker, absent coordinator, explicit stop, no eligible ready work, or exhausted quota. These are implemented limits, not instructions left to the model.

The GitHub coordinator uses the already-authorised Codex connection; the native Hermes worker holds no GitHub token. Native tools, delegation, unrelated memory and MCPs are disabled for this supplied-text specification pass.

## Verified controls

Quota reserve, attempt cap, expired-run refusal, SQLite cleanup and Windows process-tree timeout checks passed locally. The first live provider request exposed a streaming wrapper bug; do not count it as successful work. The pilot must still return a valid reviewed packet before the long run starts.

## Resume checklist

1. Read this file and the live [task board](board.json).
2. Check the exact current claim, source revisions and linked PRs; issue creation is not ownership and submission is not acceptance.
3. On the laptop, read `outputs/hermes-production/PROGRESS.md`, `COORDINATOR.md` and `state/run.json` in the existing project workspace.
4. Inspect task-specific `outbox/<task>.json` and `<task>-HANDOFF.md`, and `state/processed/<task>.json` before doing anything twice.
5. Respect the recorded deadline and local STOP file. Never start a second supervisor or silently extend the window.

## Next action

Finish the MAP-001 pilot, verify the full output and provenance, submit a review PR and release its claim. Then launch the bounded production window and coordinate remaining independent ready tasks. Do not mark the whole blueprint complete until the repository completion gate passes.

Laptop sleep/offline time prevents useful work. On resume the worker checks its absolute deadline rather than extending the run.
