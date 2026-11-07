# Tools HTTP, event and UI contract — version 1

Normative proposed implementation, not existing upstream routes. All IDs in URLs are validated before use. P0 supplies one Razor Tools panel using same-origin JSON HTTP for reads/mutations; module events only invalidate reads. Blazor methods must call the same application handlers and authorization gates, never bypass them.

## Shared protocol

Prefix `/api/modules/wh-tools/v1/maps/{mapId}`. JSON UTF-8, `Content-Type: application/json` for mutations, maximum decompressed body 16 KiB, no duplicate object keys, no unknown properties, no coercing strings to numbers, no NaN/infinity. Positive int32 core/character IDs; canonical lowercase UUID strings for module/request IDs. Timestamps are `YYYY-MM-DDTHH:mm:ss.sssZ`, exact milliseconds UTC. Revisions are nonnegative int64; persisted records start at 1, virtual absence at 0. Schema in 09 defines structural shapes; semantic constraints below also apply.

Every mutation contains requestId UUID, idempotencyKey `[A-Za-z0-9_-]{16,64}`, intentExpiresAt (server now < value <= now+10 minutes), plus operation fields. Same key means same actor/map/operation/resource/canonical payload excluding requestId; the original intent expiry remains part of the payload. A retry keeps the original deadline, key and payload. First admission after deadline is 410 INTENT_EXPIRED. A previously committed result may be read via an authorized identical retry within 24 hours even after its original deadline. Keys never reused by a client; ledger kept 90 days, result body 24 hours. Existing key after result removal is 410 RESULT_EXPIRED, never a repeated effect. Old requests cannot become new work after 90 days because their original intent deadline is expired. See transaction order in 03.

Cookie/session authentication uses the base configured SSO; never invent a second identity store or separate module login cookie. Requests are same-origin only, CORS disabled, `Cache-Control: no-store, private` on all module HTML/HTTP/errors and negotiation. All mutation handlers explicitly validate ASP.NET antiforgery token carried in `X-CSRF-TOKEN`, obtained from same-origin authenticated `GET /api/modules/wh-tools/v1/antiforgery` (request token only; no identity/token data). Missing/invalid antiforgery is 403, before mutation. Preserve base SSO cookie name/path/SameSite behavior while requiring Secure and HttpOnly on authentication cookies; verify callback tests and record any required patch. Validate Origin exactly against the privately configured public HTTPS origin for every HTTP mutation and WebSocket handshake; absent/mismatched Origin is 403. P0 browser JSON mutations go through same-origin fetch, not an unprotected Razor form exception. Offline operator commands use separate local authorization, not this HTTP bypass. No state-changing GET. Unknown map/resource on an unauthorized scope is 403 without existence disclosure; authorized absent note is 404.

Rate limit per verified actor: mutations 30/minute, reads 120/minute, stream two concurrent connections, fixed UTC minute windows. Excess returns 429 with seconds until next window in Retry-After, no side effect. A denied request cannot create unbounded per-client state. Event heartbeat is not counted as an HTTP read. Enforcement is local to the one-process P0; scaling is a new version qualification.

## Operations

| ID | Method and suffix | Body/query | Success |
|---|---|---|---|
| TO-01 | GET `/annotations` | required systemId; optional limit 1..100 default 50; optional cursor | 200 ListResult |
| TO-01 | GET `/annotations/{annotationId}` | No body | 200 Annotation |
| TO-02 | POST `/annotations` | Create: envelope, systemId, observedAt, text | 201 Annotation; Location points to read route |
| TO-03 | PATCH `/annotations/{annotationId}` | Edit: envelope, expectedRevision >=1, text | 200 Annotation with revision+1 |
| TO-08 | GET `/consent` | No body | 200 Consent, virtual revision 0 if absent |
| TO-08 | PUT `/consent` | ConsentCommand: envelope, expectedRevision >=0, enabled, expiresAt | 200 Consent |
| TO-09 | POST `/annotations/{annotationId}/delete` | Delete: envelope, expectedRevision >=1 | 200 Tombstone |
| TO-10 | GET `/grants/{targetActorId}` | Owner only | 200 Grant, virtual revision 0 if absent |
| TO-10 | PUT `/grants/{targetActorId}` | GrantCommand: envelope, expectedRevision >=0, view, annotate, expiresAt | 200 Grant |

No request accepts authorId, instanceId, mapId override, sourceKind, provenance, uncertainty, corroboration, connection ID, arbitrary URL or markup format. Map comes from route and instance from lookup. P0 create always kind=note, effectiveSource=manual, uncertainty=reported. A manual report is never independently corroborated by a client option. Unrecognized fields fail 400 rather than being silently ignored. observedAt can be at most 300 seconds in the future and at most 90 days old. Recorded time always server-derived. Display an observation with observedAt > now as “reported time ahead”; do not turn its negative age into proof of freshness. Text 1..4000 Unicode scalar values after CRLF/CR to LF normalization; reject NUL, unsupported controls except TAB/LF, invalid Unicode and all-whitespace. No trimming other content. Render as plain text; URL-looking text is inert; no embedded HTML/attachments/remote fetch. PATCH changes text only; observedAt/system/author/map are immutable. To correct those, delete and create a new record explicitly.

Contribution enabled requires expiresAt in [now+60 seconds, now+30 days]; disabled requires null. Consent revision 0 is {enabled:false, expiresAt:null}; disabled/stale consent denies create/edit. Grant capabilities are booleans. annotate=true requires view=true. Either capability true requires expiry in [now+60 seconds, now+30 days]; both false requires null expiry and revokes grant. Grant subjects are character IDs, verified through base identity, never a free-text EVE name. Enabling view/annotate requires current target base access; setting both false can revoke an existing same-map grant even after that target lost base membership. A retry reads the authorized stored result before reevaluating initial-admission-only target/expiry conditions; it still rechecks current actor permission and privacy rules.

## Results, errors and cursors

Annotation fields are id, instanceId, mapId, systemId, authorId, kind=note, effectiveSource=manual, uncertainty=reported, observedAt, recordedAt, updatedAt, expiresAt, revision, text, createdSequence. Expiry is updatedAt+90 days. Server response request correlation is header `X-Request-ID`; mutation body does not echo secrets. Delete result is {id, revision, deletedAt}, no text. Consent result is {enabled, expiresAt, revision}; Grant result is {targetActorId, view, annotate, expiresAt, revision}. No grant list enumeration in P0.

ListResult is {items:[Annotation], nextCursor:string|null}. Sort ascending immutable createdSequence then id. A protected, authenticated cursor binds actorId, mapId, systemId, initial maximum createdSequence, last emitted sequence/id, page limit, grant/owner epochs, format version and expiry now+10 minutes. Use server Data Protection purpose `WhTools.Cursor.v1`, no custom crypto. Max cursor length 2048 ASCII characters. Changed actor/filter/limit/epoch or expiry -> 400 INVALID_CURSOR after authorization. Subsequent pages omit deleted/expired notes; edits reflect current text, not a historical snapshot. This is a bounded creation window, explicitly not a transactional snapshot or durable export. Changing filters starts a fresh window. No bearer permission is carried by a cursor.

Error body exactly {requestId:UUID, code:string, message:string, current:Annotation|Consent|Grant|null}; current is non-null only for an authorized same-resource revision conflict. Delete conflict returns current Annotation only if still readable, otherwise current=null. Conflicts do not disclose a different map/actor. Codes/statuses:

| Status | Codes |
|---|---|
| 400 | INVALID_PAYLOAD, INVALID_CURSOR, INVALID_REFERENCE |
| 401 | UNAUTHENTICATED (no automatic HTML SSO redirect from module API) |
| 403 | FORBIDDEN, CONTRIBUTION_DISABLED, ANTIFORGERY_INVALID, ORIGIN_INVALID |
| 404 | NOT_FOUND (authorized missing or unregistered module route) |
| 409 | CONFLICT, IDEMPOTENCY_CONFLICT |
| 410 | INTENT_EXPIRED, RESULT_EXPIRED |
| 413 | PAYLOAD_TOO_LARGE |
| 415 | UNSUPPORTED_MEDIA_TYPE |
| 429 | RATE_LIMITED |
| 503 | BASE_UNAVAILABLE, STORAGE_UNAVAILABLE, SCHEMA_NOT_READY |
| 500 | INTERNAL_ERROR (redacted unexpected fault, never a success) |

Base membership unavailable/too old means BASE_UNAVAILABLE, not permission granted on stale evidence. Cross-map mismatches return FORBIDDEN externally; diagnostics record only non-sensitive category. Disabled dispatcher operations return MODULE_OPERATION_UNAVAILABLE internally; P0 registers no HTTP endpoint for them. Every error and fallback is secret-free and no-store. Server exception/debug details are not returned.

## TE-01 real-time invalidation and offline behavior

Dedicated SignalR hub `/hubs/modules/wh-tools/v1`, using same authenticated base actor. Only two methods: Subscribe(mapId,systemId) and Unsubscribe(). One subscription per connection; require Base + tools.view and same-map system for each subscribe. Client cannot send a group name, invoke note writes or select another actor. No general hub broadcast of private payloads.

Server message is {eventId:UUID, sequence:positive safe int64, mapId, scope:system|map, systemId:positive int32|null, type:annotation.changed|annotation.deleted|resync.required}. annotation.changed/deleted require scope=system and a positive same-map systemId. resync.required requires scope=map and systemId=null; clients refetch their current authorized system, reset cursors and reevaluate permissions. Permission/consent/owner changes increment moduleEpoch and produce only this map invalidation; no invented system ID or private grant payload is broadcast. It carries no text, actor, secret or current record. Reauthorize recipient immediately before delivery; current stale/unavailable decisions drop subscription. Permission/owner epoch change or 30-second authorization heartbeat disconnects affected connection; explicit module revoke is enforced before its success response. A reconnect always resubscribes with fresh authorization and refetches the current list. Event IDs/sequences support duplicate detection, not replay permission. No persisted client replay endpoint in P0; lost/out-of-order events cause refetch. Different connected recipients may observe events at different times. A 30-second full-list revalidation while visible closes gaps even when events are missed, counted within read limits.

Text drafts exist only in tab memory; no localStorage, IndexedDB, service-worker cache or automatic offline write queue. Network failure leaves an obvious unsaved draft in the current tab, with Retry and Clear. Explicit retry rechecks access/consent/revision and preserves intent identity. Tab close/logout/character switch clears drafts; a lost draft warning is honest. No app can erase a note someone already saw or manually copied.
