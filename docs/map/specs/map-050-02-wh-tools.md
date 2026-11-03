# WH Tools module — proposed specification

Companion to the v2 architecture. Module ID `wh-tools`; independently versioned; compatible only with explicitly tested base/bridge versions. All behavior below is proposed until implemented and qualified.

## 1. Reuse and scope

The upstream README claims shared maps, ESI tracking, signatures, routes and jump information. Validate those base functions first. Do not recreate them simply because the older new-app blueprint listed them. Our first vertical slice is **an evidence-stamped observation/note attached to an authorized mapped system**, with age/uncertainty and revocation-aware delivery.

Later tools enhance the same mapper: conflicting-scan review; stale-data explanation; uncertain-route overlays; scoped evidence export. Host provisioning, cloud billing and remote commands belong outside this module. No RIFT integration, automatic hostile detection or game control is added.

## 2. Data and capabilities

| Record | Fields |
|---|---|
| Annotation | UUID id; integer instanceId/mapId; optional integer systemId or core connection reference; kind enum note/scan-observation/jump-observation; source enum manual/core-observation/import; sourceRef optional; observedAt UTC; recordedAt UTC server-set; text; uncertainty enum unknown/reported/corroborated (proposed labels, not safety grades); revision; server-derived author; supersedesId optional same-map UUID |
| ReviewConflict | UUID id; annotation/import refs; expected/current revision; competing observed values and source times; state open/resolved; resolver identity/time; resolution reason |
| SharingConsent | actor and explicit map scope; enabled boolean default false; granted/revoked/expiry times; revision; only server-verified identity can change its own consent unless a separately authorized account-recovery process exists |

Every record references a real authorized base map; unresolved `WHInstanceId` is denied. A system/connection must belong to the same map. String content is rendered as text/sanitized supported markup, never executable HTML. Maximum lengths and retention are explicit versioned product settings; changing them requires migration/compatibility tests.

Capabilities: tools.view, tools.annotate, tools.review, tools.export and tools.manage. Each requires base access plus an explicit module grant. A map administrator does not automatically gain hosting authority. Revocation invalidates subscriptions/cache and forbids subsequent reads/exports/replay on that map.

## 3. Logical operations

Operations below are proposed module APIs; route syntax is illustrative and must be registered by the bridge. Server derives actor. Requests use a UUID requestId; mutations use idempotencyKey and updates use expectedRevision.

| ID | Operation | Input | Outcome and errors |
|---|---|---|---|
| TO-01 | Read annotations | integer mapId/systemId, cursor/filter | authorized records with source/time/uncertainty/revision; generic FORBIDDEN for denial, no other-map current body |
| TO-02 | Create annotation | map/system ref, kind/source, observedAt, text, uncertainty | one UUID/revision/event; invalid reference/type/future time rejected under documented clock tolerance |
| TO-03 | Update/resolve | annotationId, expectedRevision, patch or resolution | new revision/event; CONFLICT returns only an authorized current record; changing map/system identity is not an ordinary patch |
| TO-04 | Preview scan evidence | map/system ref and input text | normalized preview/hash and conflicts; no persistence or destructive deletion of absent rows |
| TO-05 | Commit reviewed scan | preview hash, source rows and expected revisions | atomic adapter check; applies supported base action and sidecar evidence consistently or fails; no half-written success |
| TO-06 | Explain route | authorized core route/connection refs | evidence ages, unknown mass/life, stale warnings and source refs; never a “safe route” verdict |
| TO-07 | Export evidence | explicit authorized map scope/version | redacted sidecar export plus referenced base identities; no tokens/session keys/other-map grants |
| TO-08 | Change own sharing | map scope, enabled/expiry, expected revision | consent event, immediate local invalidation and stopped module delivery; remote token revocation is separately reported |

Error vocabulary: FORBIDDEN, NOT_FOUND (only where non-leaking), INVALID_PAYLOAD, CROSS_MAP, CONFLICT, IDEMPOTENCY_CONFLICT, STALE_PREVIEW, BASE_UNAVAILABLE, MODULE_DISABLED. A repeated key with the same actor/map/operation/payload returns the original result; another payload with that key fails. Authorization is rechecked before reading a private cached result.

## 4. Typed example

Proposed TO-02 input for an authenticated editor already authorized to this map:

```json
{"requestId":"00000000-0000-4000-8000-000000000501","idempotencyKey":"tools-note-501","mapId":42,"systemId":301,"kind":"note","source":"manual","observedAt":"2026-11-02T16:00:00Z","text":"Reported movement; verify before acting.","uncertainty":"reported"}
```

The bridge looks up map 42's non-null instance and system 301's parent map; it does not trust a browser-supplied instance/actor. The response contains a UUID annotationId, revision 1 and a scoped event. A response is expected design, not an observed test result.

Invalid update example:

```json
{"requestId":"00000000-0000-4000-8000-000000000502","idempotencyKey":"tools-note-edit-502","mapId":42,"annotationId":"00000000-0000-4000-8000-000000000111","expectedRevision":1,"patch":{"text":"Updated observation"}}
```

If the authorized current revision is 2, return CONFLICT and do not overwrite it. If the actor lacks access, return FORBIDDEN without revealing the current record. These are alternative preconditions, not two simultaneous expected results.

## 5. Freshness, location and jump evidence

Always display observation time, recorded time, source and uncertainty. Proposed initial UI warning threshold: ten minutes for manually reported intel, adjustable by the operator and labelled a product display policy, not a game rule. Expiry marks a record stale; it does not prove a hole collapsed or delete audit history.

Prefer already-authorized core observations. If a missing integration requires ESI polling, use one shared gateway/cache/budget per application-character rate-limit group, not an independent module poller. E11..E14 describe a specific compatibility snapshot and caching/limits, not a universal polling frequency. Schedule no earlier than the actual cache expiry and any Retry-After/bucket delay; add bounded jitter/backoff. Do not use the snapshot's five-second cache age as an instruction to poll every five seconds.

The supplied path inventory does not evidence a personal jump-history feed. A location transition can be recorded as a derived observation only if its derivation, sampling gap and uncertainty are retained. Manual jump reports stay manual. Core jump records are inspected implementation data, not proof of complete traffic or exact remaining mass.

## 6. Workflow and failure states

Paste → preview → compare source/age/conflict → explicitly save → show committed revision. Same system/signature name is one active identity under the selected base policy; group/type changes are content. Keep historical events and reviewed supersession. Preserve base signature length initially; avoid a competing module validator.

For denied/empty/stale/offline states, say why an action cannot complete without leaking another map. Offline text is a local draft, not a committed scan. On reconnect, reauthorize, recheck consent and expected revisions; a revoked actor cannot replay an old queued write. Browser storage must exclude tokens and raw private debug logs; explicitly disclose whether local drafts persist and provide clear/delete controls.

## 7. Module lifecycle

Disabled: no Tools endpoints/events/collection, no module navigation except operator management, no base data migration. Enabling requires a compatible schema and explicit owner/grant pairing. A version mismatch fails closed for Tools while preserving qualified base functions. Uninstall preserves an operator-exportable module archive/tombstones until an explicit retention/deletion action. Core maps are not removed.

Acceptance IDs are defined in the build/test plan. The first release must demonstrate one complete source-stamped annotation workflow, cross-map denial, stale/conflict behavior, restart persistence and revocation before adding more tools.
