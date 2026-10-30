# Scheduling and Time Semantics

**Task:** MAP-007 — Define scheduling and time semantics
**Claim commit:** f2d08b1f1b9886cd97a263d47978fedd1da2e45e
**Worker:** hermes-laptop-map-007-auto-20261030
**Input revision:** 792b158838aa5214d0156690d24e21e780de542e
**Output path:** docs/map/specs/scheduling.md
**Status:** proposed map record; not accepted implementation evidence

## 1. Purpose and scope

This specification records common time semantics for operating periods, assignment expiry, backups and movement windows in the Eve Cloud build map. It defines how instants, durations, windows and recurrences are interpreted across the concept inputs. It does not define fields: field names, types, required-versus-optional distinctions and default values remain with MAP-003. Nothing here selects a scheduling library, sets a default timezone, invents a default schedule or retention, or converts an unresolved policy into a mandate.

Field ownership remains with MAP-003 per the task scope; this document concerns time semantics only.

## 2. Baseline intent from concept inputs

The pinned inputs describe intended behaviour, not available features:

- An assignment may describe its operating schedule, assignment expiry, movement window, backup schedule, destination, retention and recovery custodians (docs/CONCEPT.md).
- A Sunday maintenance window, backups every six hours, and CEO or appointed-officer recovery access are illustrative settings, not universal defaults (docs/CONCEPT.md).
- A backup button and a timed backup should use the same verified procedure (docs/CONCEPT.md).
- Scheduled backup gives predictable recovery copies; changes after the last good copy may be lost (docs/DECISION-GUIDE.md).
- Automatic movement reduces manual intervention, but stateful handover and duplicate writers are difficult and require application-specific fencing and failure tests (docs/DECISION-GUIDE.md).
- A scheduled or clicked backup records completion or failure; a successful upload is not proof of recoverability; a restore exercise is required (docs/TRUST-AND-RECOVERY.md).
- An offline host cannot make a new backup; recovery may lose changes since the most recent usable copy (docs/TRUST-AND-RECOVERY.md).
- A planned move verifies destination consent and compatibility, quiesces writes and jobs, captures consistent state, verifies the destination, changes routing and fences the previous writer before new writes are admitted; two hosts appearing healthy never justify two authoritative writers (docs/TRUST-AND-RECOVERY.md).

## 3. Stored and displayed time

### 3.1 UTC storage intent

The pinned inputs do not state a storage convention. The proposed intent for coordinator and MAP-003 review is: store instants in Coordinated Universal Time (UTC). This is an unresolved proposal, not a baseline mandate; MAP-003 decides whether stored instants are UTC, local, or both.

Display-time handling is also unresolved. Candidate rules include displaying in the requesting user's timezone, a corporation policy timezone, or UTC; none is selected by this specification. No default timezone is invented here, and no example may treat one as selected.

### 3.2 Explicit timezones

Any future-dated local time must carry an explicit timezone, preferably an IANA zone identifier such as Europe/London or America/Chicago. A fixed offset alone (for example +01:00) is insufficient because a zone's offset changes across daylight-saving transitions. Timezone and local time are a pair; neither alone forms a complete instant.

### 3.3 Daylight-saving ambiguity

Recurring windows expressed in local wall-clock time encounter two ambiguities:

- Spring forward: a local time that does not exist on the transition day (for example 02:30 when clocks jump from 02:00 to 03:00).
- Fall back: a local time that occurs twice (for example 01:30 in daylight time, then again in standard time).

Policy must decide whether a scheduled job skips, runs once at a normalized instant, or runs at both wall-clock occurrences. The decision is open; no outcome is the default in this specification.

### 3.4 Missed schedules

If a host is offline when a scheduled backup or the start of a movement window arrives, the schedule is missed. The offline host cannot make a new backup, and a missed movement window is not authorization to migrate outside the window. Policy must decide whether the platform skips the occurrence, waits for the next host-online time, or attempts a bounded catch-up run. Any catch-up run must be explicit and logged; silent double execution is not permitted.

### 3.5 Clock uncertainty

Host clocks may drift and may not agree with one another; network time is not guaranteed by the concept inputs. Movement fencing and write quiescence must tolerate clock skew between hosts. Wall-clock comparison alone must not decide which writer is authoritative. Any skew tolerance value is a pending MAP-003 field decision, not a value chosen here.

## 4. Movement window versus migration promise

A movement window is a time-based permission: it states when a move may be attempted. It is not a promise of successful automatic migration. Automatic movement remains a later capability requiring its own evidence. If destination verification fails during a window, the move stops, a tested rollback applies, and the previous host remains authoritative. Two hosts both appearing healthy never justify two authoritative writers.

## 5. Backup creation and restore verification are distinct

Scheduling semantics govern backup creation: when a scheduled or clicked backup starts, whether it runs while the host is online, and how completion or failure is recorded. Restore verification is a separate operation. A successful backup upload is not proof of recoverability; only a restore exercise demonstrates it. The backup schedule must not be treated as a restore schedule, and restore evidence must not be inferred from backup completion records.

## 6. Boundary examples

The examples use schematic field names (movement_window.start, movement_window.end, timezone, backup_schedule, assignment_expiry) pending the MAP-003 field registry. Required-versus-optional status is not decided here; no example establishes a default, and none resolves an open policy question.

**Example 1 — Weekly maintenance window.** A host offers a Sunday 02:00–04:00 America/Chicago operating period. On the spring-forward Sunday the local interval 02:00–03:00 does not exist; on the fall-back Sunday 01:00–02:00 occurs twice. The example shows why the window must be defined either as a pair of UTC instants or as a local interval with an explicit daylight-saving policy. It selects neither resolution.

**Example 2 — Assignment expiry.** An assignment carries an expiry stored as an instant; the storage convention (UTC, local, or both) is unresolved (§3.1, §7). Whether expiry blocks reads, writes or both is unresolved (§7). A policy may block writes after expiry, may block reads and writes, or may take no access action at all; this specification selects none of those outcomes. Expiry is not a movement trigger and does not start a migration.

**Example 3 — Missed six-hourly backup.** A timed backup is due every six hours. The host is offline at the third occurrence; the schedule is missed and no backup is created. The next scheduled occurrence runs normally unless policy explicitly defines a catch-up. Loss of changes since the last usable copy is a stated risk, not a hidden outcome.

**Example 4 — Failed movement inside the window.** A movement window opens at 08:00 UTC and closes at 10:00 UTC. The platform begins the move at 09:00; destination verification fails at 09:30; the previous writer remains fenced and authoritative. No second writer is admitted merely because both hosts appear healthy. The window permission expires at 10:00 without a successful move; a new attempt requires a new policy decision, not automatic retry.

Each example is bounded to time semantics and decides nothing about deployment runtime, cloud provider, cost, licence or MAP-003 fields.

## 7. Unresolved policy questions

- Storage convention: UTC instants, local instants, or both?
- Canonical timezone source and handling of timezone database updates.
- Display-time rule: requesting user's timezone, corporation policy timezone, UTC, or another rule; none selected.
- Daylight-saving resolution for recurring local windows: skip, normalize, first occurrence, or both occurrences.
- Missed-schedule policy: skip, wait for next online occurrence, or bounded catch-up.
- Maximum tolerated clock skew between hosts and how fencing uses it.
- Who may create or change a schedule, and whether hardware-owner revocation cancels pending scheduled backups.
- Whether assignment expiry blocks reads, writes, or both.
- How backup scheduling interacts with restore-exercise scheduling.

None of the above is a mandate. Each remains open for MAP-003 field work or a later policy task.

## 8. Open items outside this specification

- Selection of a scheduling library or scheduler implementation: out of scope for MAP-007.
- Field registry, types and required-versus-optional distinctions: owned by MAP-003.
- Measured restore-exercise evidence and failure tests for automatic movement: later capability tasks.
- Default schedules, retention periods and timezones: intentionally not invented here.
