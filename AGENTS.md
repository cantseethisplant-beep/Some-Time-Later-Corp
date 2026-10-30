# Production instructions

Read AI-CONTEXT.md and docs/PRODUCTION.md before doing production work. The live production/board.json is the sole task ownership record. Claim one ready task atomically and verify the claim before starting. One AI worker may have at most one active task. Do not work on backlog tasks or use unfinished tasks as inputs.

Respect each task's inputs, output paths and acceptance conditions. Preserve accepted work and reuse checks within their validity conditions. Update the shared board only with the current file SHA; a conflict means reread and reevaluate. Never force a stale claim or overwrite another owner's work.

Submission is not acceptance. Do not mark your own result accepted unless the project owner explicitly assigns you that authority. Do not implement the app, deploy, grant access or incur costs merely because a map task exists. Do not delegate to other agents without user authorisation.

For an AI without GitHub write access, follow CONTRIBUTING.md and production/forms. Give the user a completed claim-request packet and destination link; wait for a saved claim confirmation. Return completed files using the finished-work packet and submission link. Do not mistake an issue for a board claim or a submission for acceptance. The coordinator handles branch creation, board updates and release for this route.


## User-authorised autonomous blueprint follow-ups (30 October 2026)

The project owner authorised the local Hermes coordinator to continue after MAP-015 without recurring Codex check-ins. This extends the original static task list for bounded **draft production and review only**; acceptance and merging remain separate.

The local coordinator may admit one gap audit, then at most six independent follow-up drafts per batch, with explicit immutable inputs, distinct output paths, observable checks and atomic board admission/claims. Completed, released submissions may be examined as **UNACCEPTED REVIEW MATERIAL** to find contradictions and draft reconciliations. They are not accepted requirements, dependency satisfaction or verified technical evidence. A task may not consume another ready/active task's future result. This is the specific exception to the earlier accepted-input-only rule for review/reconciliation work, not permission to build from unaccepted drafts.

Native Hermes proposes a structured gap report; deterministic code restricts admission to supplied-text planning/reconciliation, assigns IDs and paths, checks available pinned sources and preserves existing board records. No model chooses credentials, execution commands, permissions or paid routes. At most two document corrections and six model-request attempts apply per task. Repeated gap keys and audit rounds are bounded to prevent an endless generation chain. Original run/daily accounting and the free-account reserve remain enforced; no counters reset.

After useful drafting is exhausted, assemble a candidate blueprint with component/data/interface map, ordered build steps, acceptance matrix, source pins and exact blockers. Do not call it accepted or build-ready. Missing owner decisions, upstream identity/version/licence verification, compatibility/resource/restore evidence or access must be reported accurately. These are not repaired by inventing facts. Independent acceptance, required technical evidence and a frozen revision still govern the completion gate.

Progress: production/HERMES-PROGRESS.md and production/handoffs/MAP-000-local-auto.md. Local resume: BLUEPRINT-LOOP.md, AUTONOMOUS-HANDOFF.md and state/blueprint-loop.json. Explicit STOP and all access/security/budget gates remain effective. No app implementation or deployment is authorised by this loop.
