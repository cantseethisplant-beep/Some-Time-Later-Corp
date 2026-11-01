# Current recovery: validated delivery and recovered-source integration

Owner instruction, 1 November 2026: repair assembly formatting/review errors, reuse saved work and produce a concrete reviewable blueprint package using free inference only without recurring Codex check-ins. This section supersedes older recovery/assembly policy below where they differ.

Root cause: review_job serialized the parsed payload as a JSON storage envelope although the producer had supplied valid BEGIN FILE / BEGIN HANDOFF sections. The critic then treated coordinator serialization as a producer formatting error. Critics now receive render_delivery's validated file sections. Complete alternative JSON transport is accepted only after task identity, exact output-path and content completeness checks and is rendered to the same review format. Critic mode has its own schema-bound system prompt without the document-extraction skill; word-count aims are not automatic content failure gates. Old rejected drafts remain excluded from critic source context. Revoked claims and scope/evidence violations still fail.

MAP-031..034 were recovered through an explicit Codex coordinator review: original raw hashes/file envelopes checked, latest generations compared with old findings, uniquely pinned SHAs expanded, MAP-032's missing proposed backup_policy_ref relationship supplied from its actual pinned sources, and MAP-034's old missing-part statements marked as historical snapshot context. Draft PRs #25–#28 disclose coordinator edits and retain native revision findings. There was no native recheck, project acceptance, merge or budget reset. Recovery spent zero Hermes requests and kept all original task counters at six.

The original MAP-034 did not consume completed MAP-031/032/033. Those are now published immutable inputs. A single new recovered-source integration contract may consume these changed inputs, with a source fingerprint and the same six-per-new-task/800-run/daily/reserve limits. It cannot be allocated when the old source set already contained the prerequisite parts, cannot consume blocked/unreleased parts, cannot create a second integration task and cannot restart a failed integration under a fresh allowance. No global audit loop is added. The unattended main loop never invokes Codex coordinator review overrides.

Package: BLUEPRINT-PACKAGE/README.md, three exact published source copies, package-manifest.json (immutable commits and SHA-256), and 04-consolidated-candidate.md once the integration draft is published. BLUEPRINT-CANDIDATE.md mirrors that published candidate. All artifacts remain unaccepted proposals with exact owner/technical-evidence prerequisites. Completed assembly is a review package, not certified build readiness or a deployed app. Completion stops at a concrete review handoff. No Codex heartbeat is installed.

Live claim readback now uses the already scoped local GitHub transport when configured, avoiding anonymous edge-cache lag after CAS writes. Credentials stay outside Git/prompts. Authentication failure does not fall back to stale public ownership. Public fallback remains only for pre-auth cases where no local credential exists. Exact ownership and path checks remain unchanged.

Verification: 139 deterministic checks pass, including actual delivery framing versus persistence envelopes, alternative JSON path/identity guards, stale critic isolation, changed-input-only integration, completed prerequisites, original ledger preservation, offline package hashes, no repeated task allocation, revoked claims and auth failure. Native output, archived critics, coordinator corrections and publication receipts remain auditable.


## Earlier policy history

# Current strategy: fixed candidate blueprint assembly

Owner instruction, 31 October 2026: fix MAP-030, stop repeated global audits and assemble a usable review package from completed work without recurring Codex check-ins. RUN.json blueprint_loop.strategy=assemble_candidate selects blueprint_assembly.py. This section supersedes older audit/replenishment instructions below for this run.

Four stages, each allocated once under a durable manifest and board CAS: build sequence/requirement traceability; component/data/interface map; acceptance/evidence/source-pin/decision matrix; consolidated candidate blueprint. Stages 1–3 share frozen completed inputs in state/assembly-inputs.json. Stage 4 also reads only completed, released assembly parts. A blocked part stays blocked, gets no fresh request allowance, and is listed explicitly rather than consumed as an input. Other independent parts may continue. The source freeze includes the latest completed audit for gap context only; its queue proposals are historical and are ignored by this strategy.

Track BLUEPRINT-ASSEMBLY.md, BLUEPRINT-LOOP.md, state/blueprint-loop.json, public production/HERMES-PROGRESS.md and linked draft PRs. BLUEPRINT-CANDIDATE.md is written from the published final draft once available. Completion stops with an explicit review handoff; a failed final part stops as incomplete. No further general audit/generator cycle is created. Draft usefulness is not verified build readiness: exact owner decisions and missing upstream/version/licence/component/restore evidence remain explicit prerequisites.

The original run/SQLite ledger, 800 total and daily caps, 100-account-request reserve, six requests and two document correction rounds per task, live-zero-price model routes and STOP/access/security gates remain enforced. No paid fallback, independent acceptance, merge, app implementation/deployment or recurring Codex schedule is added.

MAP-030 coordinator correction: pinned MAP-015 release-lifecycle.md @ 1cd788bd77c027a6808c3c4179784a77d8ca1efe was added to operations and build-and-acceptance coverage as unaccepted release/rollback/checklist context. Coverage statuses were unchanged; no checklist item is claimed performed or accepted. Native critic revision findings were retained and no further native request was spent. Draft PR #24 awaits independent project review.

Verification: 126 checks pass, including exact four-stage completion, no duplicate allocation, frozen source reuse, completed-part-only synthesis, blocked-part exclusion, missing remote source failure, stage-contract identity and truthful incomplete/final handoffs.


## Earlier policy history

# User-authorised autonomous blueprint drafting loop

Authorised 30 October 2026: keep drafting beyond MAP-015 without recurring Codex checks. The local coordinator audits coverage, admits up to six independent follow-ups per batch, re-audits completed drafts and assembles a candidate blueprint with explicit remaining blockers.

Completed, released submissions are unaccepted review objects only, never established requirements or verified technical evidence. No automatic acceptance, merge, implementation or deployment. Missing research, measurements, credentials and owner decisions remain exact blockers. The public AGENTS.md, docs/PRODUCTION.md and production/TASK-GENERATION.md record this specific review-input exception.

Free-only, live-zero-price routes; same run and SQLite ledger, 800 total attempts, 800 per UTC date, 100 account requests reserved, six requests and two document corrections per task. Maximum twelve coverage audits and three tasks per stable gap key prevent unproductive repetition. Explicit STOP and genuine access/security/budget gates remain effective.

Local resume: BLUEPRINT-LOOP.md, AUTONOMOUS-HANDOFF.md, state/blueprint-loop.json, state/auto.json and state/supervisor.json. Public board and linked draft PRs record actual ownership/submission; automated screening is not acceptance.


## Output recovery, 31 October

Complete, schema-valid native audit JSON is canonical. The coordinator renders the human-readable report and a labelled metadata handoff locally, with the original native response/hash retained. General specification files still require complete unambiguous content; missing substantive content and unknown facts are never invented. Envelope/format recovery uses no generation request or correction round. Reuse requires matching raw-response claim/run/source/hash provenance and live ownership, no STOP and a valid lease. Critic response storage is isolated by round/draft hash. An eligible blocked audit may resume its same claim atomically only if valid recoverable content and a remaining critic request exist. Original inference/correction counters and all free-only limits remain enforced.

MAP-016's malformed Markdown envelope was recovered from its valid JSON. Coordinator review excluded one impossible research-dependent catalogue proposal and recorded its exact evidence blocker; the original native content is preserved. Submission remains a draft pending independent review.


## MAP-022 coordination-reference recovery

Audit source_tasks are limited to completed documents actually supplied at immutable revisions. The worker now pins the coordination board at its claim commit separately. On gap/blocked rows only, known IDs from that pinned board may be recorded as labelled coordination-only status in existing assessment text, explicitly not supplied documents or independently verified evidence. Unknown IDs and board-only completeness claims remain rejected. Saved-output provenance binds this context. Original response bytes remain preserved, and any classification is disclosed in the handoff. MAP-022 recovery reused its existing output under the same request/correction limits; 116 regression checks pass. Native automated review and independent acceptance boundaries remain in place.
