# WHMapper module blueprint v3

Updated 3 November 2026. Creator: VelesPhylakos. Current specification: **MAP-051, draft PR #45**. The owner requested completion of the seven v2 review gaps. This is Codex-authored reconciliation of completed unaccepted Hermes research and pinned sources; no native inference or acceptance is claimed.

## Start here

[Bounded scope and readiness definitions](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-00-start.md). This v3 governs the selected P0 scope and supersedes contradictory design policy in v2/v1. Research/source evidence remains version-bound.

| Document | Purpose |
|---|---|
| [01-ACCESS-AND-CONSENT.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-01-access-and-consent.md) | Separate read/contribution consent, grant matrix, owner pairing/transfer/recovery |
| [02-TOOLS-CONTRACT.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-02-tools-contract.md) | Exact HTTP/events, errors/limits, cursor and offline behavior |
| [03-DATA-AND-TRANSACTIONS.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-03-data-and-transactions.md) | Schema, transactions/idempotency, outbox, deletion and retry-body privacy |
| [04-SCAN-AND-FUTURE-SCOPE.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-04-scan-and-future-scope.md) | P0 sidecar-only writes and precise later-feature boundaries |
| [05-RECOVERY-AND-MIGRATIONS.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-05-recovery-and-migrations.md) | Durable key ring, migration ownership/readiness, backup/journal/restore targets |
| [06-BUILD-AND-QUALIFICATION.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-06-build-and-qualification.md) | Nine build steps, twenty-five future qualification checks, selected release sets |
| [07-HOSTING-READONLY.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-07-hosting-readonly.md) | Optional metadata ledger, explicit roles/approvals and no provider effects |
| [08-REVIEW-AND-SOURCES.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-08-review-and-sources.md) | R01..R07 dispositions, required patch inventory and primary source record |
| [09-CONTRACT-SCHEMA.md](https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/blob/58dc0f5d39b88949d5b33e96a7522cfc3f100b37/docs/map/specs/map-051-09-contract-schema.md) | Twelve JSON schema definitions and forty-seven contract fixtures |

## What is specified

P0 reuses the pinned WHMapper and adds manual system notes with source/time/age, revisions/conflicts, grants/consent, deletion, invalidations and recovery. Hosting remains a disabled-by-default optional offers/request/approval ledger. It does not deploy anything. Combined scan writes, provenance/corroboration automation, route overlays/export and provider execution are explicitly later scope. Exactly two user-facing modules use a maintained compile-time bridge. Integer core IDs remain unchanged.

Design defaults are explicit, not invented provider facts: contribution consent controls new contributions, reading uses separate permission; prior notes have declared retention; owner recovery is defined; durable keys and off-host deny/delete journaling are required for the selected live profile. The operator must acknowledge actual live-data/availability policy and supply private configuration before live use. Oracle remains a conditional origin behind Cloudflare; current account/region/quota/ARM/domain/backup conditions are checked only for that deployment.

## Checks and honest remaining gates

The seven review findings now have concrete specification dispositions. **152 document/schema/fixture checks passed**, including **47 valid/invalid contract fixtures** across **12 schema definitions**. Exact UTF-8 output readback verified for all ten files. These are specification checks, not app tests.

**Repository build-ready completion has not passed.** Independent acceptance and required exact dependency/licence/asset/baseline/bridge evidence remain. This laptop currently has no listed .NET SDK and no Docker command, so no untouched-base compile, app run, migration/security/restore or ARM/capacity qualification is claimed. The twenty-five Q checks are NOT_RUN. No owner policy/account values are fabricated.

Next concrete work is P0-B00..02 in an authorised isolated build environment, not another general research/audit cycle. A failed check revises only the affected contract/evidence. No app/cloud implementation, existing-server access, costs, native worker restart or merge occurred. The Hermes counter remains 255/800; this document work used zero new Hermes calls.

## Frozen identities and downloads

- Blueprint draft: https://github.com/cantseethisplant-beep/Some-Time-Later-Corp/pull/45; output commit `58dc0f5d39b88949d5b33e96a7522cfc3f100b37`.
- [v3 source manifest](WH-BLUEPRINT-V3-MANIFEST.json) records each immutable source path/hash.
- Offline review artifact: `WH-BLUEPRINT-V3-REVIEW.zip`, 34 allowlisted files, SHA-256 `032df2c7d207e3229fbf9b36ec51e1703fd832dde95ab343ea3838bb8768ebe7` (available from the creator; not uploaded as an arbitrary public binary).
- [Previous v2 guide](WH-BLUEPRINT-V2.md) and [v1 guide](WH-BLUEPRINT-V1.md) are historical.
- [Completed research handoff](research/RESEARCH-HANDOFF.md) retains source statuses and limitations.

Submission is not independent acceptance. See [production rules](../PRODUCTION.md) and the live [task board](../../production/board.json).
