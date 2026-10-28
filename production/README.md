# Live production queue

The authoritative queue is [board.json](board.json). Follow [the production rules](../docs/PRODUCTION.md) to claim one task atomically before working. Filter status=ready to find work that can start now. Backlog and review tasks are not claimable.

The initial five tasks need no external research or runtime testing: they formalise existing concept requirements. Their acceptance checks are clarity, coverage, consistency and explicit uncertainty. Technical research and component tests will have their own scoped tasks later where necessary.

Do not edit this summary to announce ownership; only a verified board claim reserves a task. No task is currently claimed by the repository-setup assistant.
