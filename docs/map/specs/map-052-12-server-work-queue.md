# Proposed server work queue and ownership/evidence protocol

This is a handoff design, not a running queue or authorization to launch agents. It does not import laptop claims, reset the Hermes ledger or start a supervisor. Each row becomes actionable only through the server's existing authorised coordinator after intake and admission checks.

## Board authority

Public `production/board.json` remains the sole owner record for **MAP planning tasks**, including MAP-052. Future private **BUILD implementation tasks** use `Eve-Cloud/production/build-board.json`, a separate namespace and authority. Never represent one BUILD task as claimed on two boards or use a public MAP claim as private execution permission. Public progress may summarize safe BUILD states/PR links without hosting a second ownership lock or private evidence. If the server already has a native authoritative queue for this project, the coordinator chooses that queue at intake and writes an explicit authority adapter record; do not run two claim services in parallel or infer access to unrelated Work Rails projects.

Initial board is absent until created by the authorised coordinator. Admission is data validation plus a task record, not an AI's promise in chat. Each task has id, title, scope, mode review/preflight/build/verification, accepted input commits/digests, dependsOn, allowedPaths, command/effect limits, acceptanceCheckIds, requiredEnvironmentProfile, budget/deadline, authorityReference, status, claim and submission. Unknown/missing required fields block admission. Never set ready because an upstream task is merely review/claimed or likely to finish soon.

## Finite proposed tasks

IDs below are stable proposal names; intake assigns native queue IDs and records the mapping once. All tasks start PLANNED, not already ready/claimed.

| Proposal | Mode | Existing inputs / dependencies | Output and completion rule |
|---|---|---|---|
| SV-01 Independent specification review | review | Immutable completed v4 and pinned primary evidence, used as unaccepted review material | Focused review with contract/source references, severities and scoped acceptance/rejection; no implementation |
| SV-02 Server intake preflight | preflight | Same immutable handoff + existing server permissions; no SV-01 output needed | Private environment receipt with observed/unavailable values; no installations or account changes |
| SV-03 Existing capability/roadmap worksheet | review | Same immutable v4 + pinned upstream/source packets; no other proposal output needed | Matrix base claimed/source-inspected/tested, P0 addition, later requirement/exclusion and exact next design gap; no new architecture guessing |
| SV-04 Baseline and locked inputs | build | Accepted SV-01 and SV-02, recorded build authority | P0-B00/B01; untouched upstream compile/fixture tests and lock/licence/image evidence; architecture explicit |
| SV-05 Bridge and migration/key spike | build | Accepted SV-04, accepted exact v4 requirements | P0-B02; actual hook inventory, both modules off baseline, readiness/key/lock/identity checks |
| SV-06 Tools storage/API slice | build | Accepted SV-05 | P0-B03 with contract vectors/concurrency/privacy tests and draft private PR |
| SV-07 Tools UI and real-time | build | Accepted SV-06 | P0-B04 with fresh/unsaved/conflict/deletion/access state fixtures |
| SV-08 Optional Hosting ledger | build | Accepted SV-05; explicitly selected in release | P0-B06 and Q23; no dependency on unfinished Tools UI; no remote effects |
| SV-09 Operating/recovery qualification | verification | Accepted selected Tools/bridge artifacts + private qualified recovery profile | P0-B05, Q17..Q22/Q25 as applicable, real restore and laptop-off operation evidence |
| SV-10 Optional cloud pilot qualification | verification | Accepted SV-09, selected deployment authority/account/domain profile | P0-B07/Q24; provider cost/eligibility checks; actual publication/provisioning only under that authority |
| SV-11 Release record | review | Accepted selected implementation/evidence, no outstanding in-scope blockers | P0-B08; independent release decision, exact included/deferred scope, operator runbook |

SV-01/02/03 are independent intake proposals from existing materials. At most one is active per worker. SV-06 and SV-08 could proceed independently after accepted bridge evidence **only if** allowed output paths and shared migration/integration ownership do not overlap; otherwise coordinator serializes them. Do not place pending dependencies in the executable ready queue. Failed review produces one concrete remediation task scoped to that failure, not an unbounded audit generator.

## Atomic claims, fencing and branch isolation

For a Git-backed BUILD board: fetch the current blob SHA, verify ready inputs/authority/budget and no other active claim for this worker, generate workerId+claimToken+monotonic claimGeneration, update with exact SHA, reread and verify ownership before work. A conflict/timeout means reread and resolve the outcome; never force a stale board. Branch/worktree is task-specific and records input revision. Completion, review and release writes compare current claim token/generation. No claimed task is stolen on elapsed time; coordinator checks existing artifacts/processes, records explicit revocation and increments generation before reassignment.

For a native queue, its authoritative compare-and-swap/fencing transaction must provide equivalent ownership; record its durable task and spent-intent identities. This blueprint does not permit bypassing native busy/admission fences, reusing a consumed intent or widening existing permissions. Validate queue adapter capabilities during intake; if absent, keep tasks PLANNED and report the exact missing gate.

Claims are cooperative source coordination, not a cryptographic isolation boundary. An old worker must recheck immediately before publishing and stop if revoked; only the coordinator/reviewer with the current generation may integrate. Worktrees reduce accidental collisions; shared paths/migrations are still serialized. No worker may merge/accept its own draft. Private PRs retain input/claim/evidence identities. If GitHub write access is missing, use a copy/paste work packet and coordinator confirmation; no credentials go in that packet.

## Result and review receipt

Submission fields: taskId, workerId, claimGeneration, inputManifestHash, source/outputCommit, changedPaths, checkResults, evidenceIndex, remainingIssues, nextStep, proposedStatus and releaseClaim. Each check result is {checkId, state, expected, observedSummary, artifactHash, privateArtifactPath, environmentProfileHash, observedAt}. States NOT_RUN/PASS/FAIL/BLOCKED/NOT_APPLICABLE; N/A requires a scoped justification. Raw logs/protected fixtures stay private; public summaries omit real corporation data, addresses, credentials and device inventories. A result requires actual observed output, never the test specification copied into observedSummary.

Verifier may run defined checks under task authority; reviewer accepts/rejects against criteria independently of author. Acceptance records accepted output revision/evidence validity. Reviewer's independence is task-relative, not a claim that model criticism proves security. A passing schema check is labelled specification evidence. Required component/runtime checks still need actual execution.

## Budget, stop and recovery

Existing server model-route/spending/permission controls remain authoritative; this document grants no quota, paid fallback or privilege expansion. The coordinator sets an explicit per-task request/time bound and reserves room for verification/repair before admission. Diagnose format/transient errors and use bounded same-task repair; preserve attempt/claim history and prior outputs. On exhausted budget, owner STOP, revoked access/claim, missing required supervisor or no eligible task, checkpoint and release only owned work. Do not keep generating tasks or reset identities to evade a stop. Future progress is read from durable private handoff/CURRENT.md plus the authoritative queue, without laptop or recurring Codex check-ins.
