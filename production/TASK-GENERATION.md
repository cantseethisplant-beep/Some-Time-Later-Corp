# Generate the next task batch

This is a bounded queue-planning job, not permission to run new workers or implement the app. A generator claims one task like any other AI.

## Inputs and scan

Read the live board, production rules, map index, accepted deliverables, and relevant open submissions before proposing work. Record the board revision and source commits used. A newer live board may reveal duplication or claims; it does not make unfinished results acceptable inputs.

Find the highest-impact gaps in the build-ready completion gate. Prefer resolving a real build blocker or supplying missing acceptance evidence. Reuse accepted evidence within its validity conditions.

## Output

Propose at most six small tasks per batch. Each proposal must include:

- A unique provisional ID, title, purpose and exact output paths.
- Existing immutable input revisions and paths, with evidence type.
- Dependency task IDs and their current statuses.
- Precise scope, exclusions, completion checks and required access/tools.
- Whether external research or runtime tests are actually required.
- Proposed status: ready-candidate or backlog, with the reason.
- Duplicate/conflict check against ready, claimed, review, blocked, accepted and existing backlog work.
- A short explanation of which map gap it closes.

An input dependent on an unresolved decision, missing access, unfinished task or unavailable test environment means backlog. Keep all proposed outputs distinct from each other and from existing work. Path comparisons include parent/child paths, not just exact filename equality. Different paths can still duplicate the same deliverable; check purpose as well.

Do not invent source versions, resource measurements, compatibility or successful tests. A technical validation task must name a concrete question and observable checks, rather than ask for broad research or mass testing.

## Admission and replenishment

The generator writes a proposal file only; it does not directly add tasks, promote candidates, accept its own work or spawn AIs. The coordinator checks the proposal against the latest board and integrates approved tasks using the board file's current SHA. Preserve all concurrent claims and history. Allocate final IDs at admission to avoid collisions.

Only ready-candidates with all inputs accepted and accessible are promoted. Keep dependent tasks in backlog with explicit dependencies. After an accepted task closes a gap, reassess only its newly enabled follow-ups.

After each accepted generator batch, the coordinator may enqueue one new generator task with a new ID and output path if a meaningful map gap remains. Trigger replenishment when fewer than five unclaimed ready tasks remain or a newly accepted result unlocks important work. This is a documented manual trigger, not a running automation.

Use at most one ready or active generator task at a time. Do not make chains whose only purpose is generating more generators. Each batch must identify a build-map gap it advances. If no independent useful task is available, report that clearly and identify the exact blocker.

Stop generating when the map completion gate passes; propose a final coverage/freeze review instead. Queue size is not a measure of readiness.
