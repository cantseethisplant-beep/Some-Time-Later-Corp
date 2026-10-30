# Production rules

## Purpose

Turn the concept into an actionable build map through small, checked increments. Research and component validation belong in map tasks when needed. Building later should consume accepted decisions and evidence rather than repeat discovery. Targeted integration, environment and deployment checks remain necessary for the actual app.

## One authoritative board

`production/board.json` is the source of truth for task status, ownership and inputs. Issues and pull requests may discuss work, but do not allocate ownership. Public workers need only public inputs; private evidence must have a safe public summary if a public task depends on it.

States: `backlog` -> `ready` -> `claimed` -> `review` -> `accepted`. A task can enter `blocked` when its declared inputs prove insufficient. Rejected submissions return to `claimed` for their owner or are explicitly released to `ready`. Accepted work is reopened only with a recorded reason.

## Ready queue admission

A coordinator admits a task only when every required input already exists at an accepted immutable revision, the deliverable and checks are explicit, and its permitted output paths do not overlap any other ready or active task. No ready task may depend on the output of a ready, claimed, review or blocked task. Backlog tasks can describe future dependencies; they are not available to claim.

Every task must fit one focused work session. Split it if it requires a broad exploration, multiple unrelated outputs or an undecided input. Tasks record `depends_on`; only accepted IDs may appear there when the task is ready. All initial tasks use the existing concept documents as their user-approved intent baseline; the baseline is not technical compatibility evidence.

## Atomic claim procedure

GitHub's Contents API requires the current file blob SHA to update an existing file. Use that compare-and-swap operation on the single board file. In this chat's GitHub connector, fetch_file returns that SHA and update_file accepts it as sha. This is the claim gate; do not use a blind branch ref update as a substitute.

1. Fetch production/board.json from main, including its current blob SHA.
2. Validate that the task is ready, its dependencies are accepted, its inputs are present, and output paths do not overlap another ready/active task. Reject the claim if the worker already owns a claimed task or an unreleased review claim.
3. Generate a unique claim token and worker ID; set status to claimed, fill the claim fields and increment board_revision. Keep every unrelated record unchanged.
4. Update the board with the exact fetched sha. A conflict means no claim: reread the latest board and revalidate. Never retry with stale contents or force an overwrite.
5. Fetch the saved board and verify your token and ownership. Only then start work. If a write times out, reread and resolve its outcome before retrying.

Simultaneous updates to this one board are serialised by GitHub's file SHA check. The protocol also checks different tasks against the one-task-per-worker rule. This is a cooperative production workflow, not a security lock against administrators or clients that deliberately ignore it. No autonomous queue service is installed.

An AI without repository write access needs the user or coordinator to perform the same claim procedure and provide the saved claim. Do not start while waiting.

## User-mediated claims and submissions

[CONTRIBUTING.md](../CONTRIBUTING.md) and [production/forms](../production/forms) provide the route for AIs without GitHub access. A user posts the AI's claim request through the issue form or relays it to an authorised coordinator. Only the coordinator's verified atomic board update grants ownership; the issue, request timestamp and GitHub assignee do not.

The coordinator returns a confirmation with the saved board revision/commit, task, worker, token, permitted paths and pinned inputs. The AI verifies it directly or through a user-supplied matching current board entry. The user later submits the full finished-work packet with file contents or retrievable attachments. Incomplete multipart packets remain pending.

For this route, the AI drafts only; the coordinator creates the work branch and records the resulting issue/commit/PR in the board's submission record. Thus a producer without GitHub access is not required to supply a commit/PR before handoff. The coordinator checks ownership, scope, provenance and completeness before moving to review. Existing review/acceptance rules remain in force. Explicitly record claim release before the worker takes another task.

This is a manual inbox, not an installed automation. No credentials need to be shared.

## Claims and abandoned work

Claims do not expire automatically. Record last activity and a suggested review-after time if useful; elapsed time alone never transfers ownership. The owner may release a task through an atomic board update, recording any draft. A coordinator may reclaim abandoned work only after checking existing branches/submissions and recording revocation. An old owner must reread the board before publishing and stop if its token was revoked. Work from a revoked claim cannot be accepted without reassignment and review.

## Work, submission and acceptance

Work in an isolated branch and limit changes to the task's output paths. The branch starts from the recorded input revision. Do not silently change the task's scope or accepted inputs. If an input is missing, mark blocked, document the exact missing fact and stop dependent work; the coordinator can split or requeue it.

Submit the result with a claim token, input revisions, checks performed, evidence locations, limitations and a commit/PR reference. Update the board atomically to review and record the submission. If review work is complete, set claim.released_at explicitly before claiming another task; the task stays in review and cannot be claimed by another producer.

The project owner or an explicitly appointed reviewer accepts the result against its task criteria. Acceptance includes integrating the deliverable into main, checking that the claim is valid, recording the evidence and accepted revision, and updating the map index. Keep a task in review until integration and recording are finished. Acceptance is not a new user-permission requirement for every ordinary edit; it is a production quality state. An AI does not appoint itself reviewer of its own output.

## Reuse and revalidation

Each accepted map record must identify what is established, the source/commit/version, applicable environment and assumptions, check type, result, limitations and invalidation triggers. Mark unsupported sections unresolved. Documentation review cannot stand in for a restore test or measured resource test.

Reuse accepted evidence while its conditions hold. Reopen only affected records if versions, interfaces, deployment targets, trust assumptions or evidence change, or a concrete failure contradicts them. Record downstream impact. Do not require blanket research, mass testing or repeated user confirmation of settled choices.

## Completion gate

The map is build-ready only when its scope is bounded; all in-scope requirements have implementation steps and acceptance checks; upstream identities/versions/licences and dependencies are resolved; interfaces, roles, data, hosting, recovery and rollout decisions are consistent; required component evidence exists; and no build-blocking unknown remains. Record a frozen map revision. Actual build integration and deployment checks follow that revision and its declared environment.

## Queue expansion and task generation

Follow [TASK-GENERATION.md](../production/TASK-GENERATION.md) for bounded proposal batches, duplicate checks, admission and replenishment. Generators write proposals; coordinators admit work against the latest board. There is no automatic scheduler running. Keep one generator ready/active at a time and stop when the map completion gate passes.

Start each isolated work branch from current main after claiming, while reading task inputs at their pinned revisions. This preserves current production instructions without treating newer unfinished deliverables as accepted inputs.


## User-authorised autonomous blueprint follow-ups (30 October 2026)

The project owner authorised the local Hermes coordinator to continue after MAP-015 without recurring Codex check-ins. This extends the original static task list for bounded **draft production and review only**; acceptance and merging remain separate.

The local coordinator may admit one gap audit, then at most six independent follow-up drafts per batch, with explicit immutable inputs, distinct output paths, observable checks and atomic board admission/claims. Completed, released submissions may be examined as **UNACCEPTED REVIEW MATERIAL** to find contradictions and draft reconciliations. They are not accepted requirements, dependency satisfaction or verified technical evidence. A task may not consume another ready/active task's future result. This is the specific exception to the earlier accepted-input-only rule for review/reconciliation work, not permission to build from unaccepted drafts.

Native Hermes proposes a structured gap report; deterministic code restricts admission to supplied-text planning/reconciliation, assigns IDs and paths, checks available pinned sources and preserves existing board records. No model chooses credentials, execution commands, permissions or paid routes. At most two document corrections and six model-request attempts apply per task. Repeated gap keys and audit rounds are bounded to prevent an endless generation chain. Original run/daily accounting and the free-account reserve remain enforced; no counters reset.

After useful drafting is exhausted, assemble a candidate blueprint with component/data/interface map, ordered build steps, acceptance matrix, source pins and exact blockers. Do not call it accepted or build-ready. Missing owner decisions, upstream identity/version/licence verification, compatibility/resource/restore evidence or access must be reported accurately. These are not repaired by inventing facts. Independent acceptance, required technical evidence and a frozen revision still govern the completion gate.

Progress: production/HERMES-PROGRESS.md and production/handoffs/MAP-000-local-auto.md. Local resume: BLUEPRINT-LOOP.md, AUTONOMOUS-HANDOFF.md and state/blueprint-loop.json. Explicit STOP and all access/security/budget gates remain effective. No app implementation or deployment is authorised by this loop.
