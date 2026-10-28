# Live production queue

The authoritative queue is [board.json](board.json). Follow [the production rules](../docs/PRODUCTION.md) to claim one task atomically before working. Filter status=ready to find work that can start now. Backlog and review tasks are not claimable.

Fifteen initial work packages are defined. They formalise the concept, operating rules and evidence requirements using existing public inputs. No external research or runtime tests are required for these packages. A task being accepted as a specification does not prove the eventual app or component works.

MAP-012 proposes up to six further tasks using [TASK-GENERATION.md](TASK-GENERATION.md). Generators submit proposals; a coordinator admits independent work and keeps unmet dependencies in backlog. Replenishment is a documented manual process, with no background worker or recurring automation installed.

Read [the map index](../docs/map/INDEX.md) for the package list. Use the live board for current ownership and status; this summary does not reserve tasks.
