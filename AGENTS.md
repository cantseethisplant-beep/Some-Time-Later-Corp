# Production instructions

Read AI-CONTEXT.md and docs/PRODUCTION.md before doing production work. The live production/board.json is the sole task ownership record. Claim one ready task atomically and verify the claim before starting. One AI worker may have at most one active task. Do not work on backlog tasks or use unfinished tasks as inputs.

Respect each task's inputs, output paths and acceptance conditions. Preserve accepted work and reuse checks within their validity conditions. Update the shared board only with the current file SHA; a conflict means reread and reevaluate. Never force a stale claim or overwrite another owner's work.

Submission is not acceptance. Do not mark your own result accepted unless the project owner explicitly assigns you that authority. Do not implement the app, deploy, grant access or incur costs merely because a map task exists. Do not delegate to other agents without user authorisation.

For an AI without GitHub write access, follow CONTRIBUTING.md and production/forms. Give the user a completed claim-request packet and destination link; wait for a saved claim confirmation. Return completed files using the finished-work packet and submission link. Do not mistake an issue for a board claim or a submission for acceptance. The coordinator handles branch creation, board updates and release for this route.
