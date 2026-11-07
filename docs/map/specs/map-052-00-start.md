# WHMapper module blueprint v4 — server-AI implementation handoff

Creator: VelesPhylakos. Date: 7 November 2026. Task: MAP-052. Author: Codex, using completed but unaccepted Hermes research and pinned primary source. This revision carries forward the v3 contracts, corrects the gaps listed in 11, and prepares future server-AI work; it is submitted for independent review, not self-accepted.

## Authority and meaning of readiness

This folder is the normative v4 specification for the bounded P0 release described below. Where v3/v2/v1 or historical hosting-first material conflicts, use these v4 contracts for P0. Server handoff documents 10..12 are part of the same version. Old research remains source evidence at its own version; proposals do not become observed facts. The user authorised finishing the blueprint, not building/deploying the app, accepting service terms or spending money. Numeric policy choices in this package are selected engineering defaults, explicitly identified here, rather than guessed provider/game facts or claims that the owner has approved a live-data policy.

There are three distinct gates:

| Gate | Meaning | Current evidence |
|---|---|---|
| Specification completeness | Bounded behavior, contracts, failure rules, build order and test oracles are defined | Checked by the accompanying document/schema/fixture review |
| Build admission under the repository completion rule | Independent review plus required resolved inputs and baseline/component evidence are present | NOT passed: dependency resolution, licences/assets, untouched-base/bridge viability still require an authorised isolated build |
| Release/deployment qualification | Actual assembled app passes access, security, migration, restore, capacity and selected cloud checks | NOT run; no app or cloud deployment exists from this work |

A builder can follow this specification without inventing P0 behavior. This does not promise that unbuilt software already works, the full future product is specified, or Oracle has capacity. Stop at the exact gate on failure; update only the affected contract/evidence. Never silently substitute a new upstream release or an architecture.

## Frozen scope

Base: `pfh59/eve-whmapper` commit `2a493fad9acec9a8e15b619f7943ae8b6e7f30da`, retaining MIT notice. Compile-time Tools and Hosting libraries plus a maintained integration bridge; no claimed hot plugin ABI. Base integer IDs stay unchanged; module IDs are UUIDs. Future implementation stays in private `Eve-Cloud`; concept/specifications and safe evidence stay in public `Some-Time-Later-Corp`.

**P0 includes:** existing mapper baseline; Tools system notes created by a verified character; source/time/age labels; read/list/create/edit/delete; optimistic conflicts; explicit per-map grants; contribution consent; invalidation events; restart, backup and restore; disabled-by-default modules; optional read-only Hosting offers/request/approval ledger. No ESI polling is added by Tools. Notes never change base maps, signatures, routes, ownership or jump logs. Source is manual and uncertainty is fixed to reported in P0; unknown/corroborated labels are not selectable API values.

**Explicit later scope:** scan imports/combined core writes, core-observation ingestion, corroboration automation, route overlays, portable export, provider execution, donor-agent enrollment, billing/ISK income, scheduling/movement and multi-node orchestration. They are not implemented implicitly through P0 APIs. The retained base may already have related functions; validate/reuse them rather than rebuilding them. RIFT is excluded.

Topology: users → Cloudflare HTTPS/named Tunnel → selected private origin → WHMapper/bridge/Tools → private PostgreSQL and Redis. Hosting may be disabled even when Oracle is the origin. A single-origin pilot is not HA. The server AIs are the future build team. Server identity/capabilities must be observed there at handoff; this document work does not connect to or launch them. The production origin and recovery receiver are separate deployment roles, not automatically the AI build server. The laptop has no required build, runtime, queue, backup or journal role.

## Reading and build order

1. `01-ACCESS-AND-CONSENT.md`: identity, owner pairing, permissions, consent and revocation.
2. `02-TOOLS-CONTRACT.md` and `09-CONTRACT-SCHEMA.md`: exact HTTP, event, validation and JSON contracts.
3. `03-DATA-AND-TRANSACTIONS.md`: storage, concurrency, idempotency, outbox and deletion.
4. `04-SCAN-AND-FUTURE-SCOPE.md`: explicit boundaries for later features.
5. `05-RECOVERY-AND-MIGRATIONS.md`: keys, migrations, backup, restore and operating targets.
6. `06-BUILD-AND-QUALIFICATION.md`: ordered work and exact future pass/fail evidence.
7. `07-HOSTING-READONLY.md`: optional ledger with zero provider effects.
8. `08-REVIEW-AND-SOURCES.md`: dispositions, source pins and remaining environment/evidence gates.

Runtime secrets, live player data, account/domain identifiers and actual backup paths must be supplied through private deployment configuration, never inserted into the public specification. Missing configuration is an explicit startup/preflight failure, not an invitation to guess. The accompanying manifest binds every delivered byte and source revision. Read 10-SERVER-AI-HANDOFF.md for the portable intake prompt, 11-GAPS-AND-DISPOSITIONS.md for residual evidence/decisions, and 12-SERVER-WORK-QUEUE.md for a dependency-safe proposed queue. No laptop SDK or Docker installation is required for this planning/handoff phase.
