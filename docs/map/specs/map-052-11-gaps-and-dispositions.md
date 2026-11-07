# Focused gap review — v3 to server handoff v4

Reviewed 7 November 2026 by Codex. Findings below are from actual contract conflicts/omissions and the owner's server direction. Fixed means corrected at specification level; no runtime pass or independent acceptance is inferred. The earlier R01..R07 remain traceable in 06/08. This is one bounded review/reconciliation, not another open-ended audit loop.

| Gap | Finding / consequence | v4 resolution | Future evidence |
|---|---|---|---|
| G01 | Laptop missing tools treated as a project blocker; no actual server intake contract | 00/06/10 assign future build work to server AIs, define read-only preflight and separate build authority | SV-02 private observed preflight; no fabricated installed tools |
| G02 | Laptop backup/journal default would make live privacy actions fail when laptop shuts down | 05/10 require a qualified independent always-on recovery role; laptop is optional offline extra copy | Q19/Q20 plus laptop-off qualification; actual destination/custody still an input |
| G03 | Journal preparation preceded committed-key lookup and deadline/revision validation, potentially recording denied or replayed deletes | 03/05 validate initial intent before preparing any journal effect; matching replay returns saved result; prepared same-intent reconciliation distinct | Stale/expired/changed-payload/replayed delete has zero new append; admitted uncertain result reconciles same UUID |
| G04 | Multi-character operations lacked a complete lock order | 01 defines all characters ascending, then maps ascending, reverse release; instance set snapshot/retry | Concurrent owner/grant/revoke/unlink fixtures show no lock inversion |
| G05 | Positive-only systemId event schema could not represent map-wide permission changes | 02/03/09 define map resync with null system and system annotation events with positive target; epoch changes explicit | New schema fixtures; Q10/Q13 runtime delivery/reconnect |
| G06 | Disabling all module jobs conflicted with mandatory retention and could retain text indefinitely | 03 separates private version-matched maintenance from disabled product jobs; mismatch is visible retention fault | Q21 runs with module on and off, scrubs intent/history text too |
| G07 | Target-current-membership requirement could prevent revoking an old grant after the target left | 01/02 require current target access only for enabling; existing same-map revoke remains available to authorized manager | Grant/revoke fixture after target membership loss |
| G08 | Hashing rules lacked cross-language golden bytes; virtual revision-zero schema allowed enabled state | 03/09 supply exact format, vectors and stricter absent-record states | Contract vectors and schema fixtures here; independent C# implementation must reproduce them |
| G09 | Append-only journal had no export/checkpoint/pruning contract for restore | 05 defines separate recovery identity/export, authenticated head, backup anchor and minimum retained tail | Q20 missing-tail/anchor/reset and valid-chain restore cases |
| G10 | Server ownership/evidence/resume/failure protocol and independent ready queue not specified | 10/12 define private BUILD authority, public MAP separation, immutable task inputs, CAS claims, verifier/reviewer results and checkpoints | Server coordinator intake before admission; no task launched by this package |
| G11 | P0 described uncertainty as reported/unknown while actual create/schema fixed reported | 00 agrees with 02/09: P0 manual/reported only; other provenance labels deferred | Caller cannot select unknown/corroborated or impersonate core data |
| G12 | One-process locking and limits were assumed without a concurrent-start/deployment rule | 06 adds launch guard, stop-before-replace and lock-loss behavior; multiple AI workers do not imply runtime replicas | Q25 concurrent process/start/upgrade evidence |

## Remaining gates and bounded follow-ups

| ID | Type / stage | Required input or work | Owner / effect |
|---|---|---|---|
| O01 | Acceptance, before implementation | Independent v4/source review and recorded build authority | Server reviewer/coordinator; no self-acceptance |
| O02 | Environment, before baseline | Observed build host identity/tooling/repository access/isolation and supported architecture | Server intake; laptop inspection is irrelevant |
| O03 | Component, baseline | Exact resolved SDK/dependencies/locks/images, full applicable licence/asset inventory and clean upstream build | Server baseline task; no legal approval inferred from root MIT |
| O04 | Integration, before feature qualification | Actual bridge seams, base mutation hooks, membership freshness metadata, key migration and process fencing | Bridge task; new design requirements are not existing upstream facts |
| O05 | Scope, before later milestones | Map desired WH features to verified existing base capability, P0 addition, planned later design or explicit exclusion | Focused capability worksheet SV-03; avoid treating a notes slice as the whole product |
| O06 | Live policy, before real data | Retention/contribution behavior, operator/recovery custody, backup/journal availability and support acknowledgment | Owner/operator; fixture environment uses synthetic data |
| O07 | Cloud, only if selected | Current Oracle account/home region/quota/capacity and ARM image/proxy/SSO/domain/backup cost evidence | Deployment owner; free-only spending policy preserved |
| O08 | Runtime, selected release | Actual Q checks with pinned inputs, outputs and invalidation conditions | Server verifier/reviewer; all remain NOT_RUN here |

O01..O08 are specifically owned prerequisites, not facts to guess or duplicate research topics. Oracle/Cloudflare facts from the earlier dated source packet were not refreshed because no provisioning decision is being made here. An outdated or incompatible pin is reported with the affected contract; a new upstream revision requires a deliberate versioned change, never a silent “latest” upgrade.

## Future product coverage

P0 is the bounded first slice over an existing mapper; it does not complete every tool/hosting ambition. SV-03 inventories base maps, signatures/paste, routes/jump information, notes, access, tracking, and operational deployment from the pinned source. Record source-only versus tested state. Later advanced Tools and Hosting execution get their own concrete design task only when required inputs exist. Do not inflate feature completion with repeated prose audits, or let optional hosting automation block the first useful WH tool. RIFT stays excluded.
