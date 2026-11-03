# Identity, access, sharing and owner lifecycle

Normative P0 design choices; source behavior is identified separately in 08. All times are server UTC. A character ID is a verified positive EVE character integer, not an account name, browser UID, corporation ID or client-submitted author. Use exactly the current verified base character for a Tools session; switching character clears module subscriptions/drafts/cursors and reauthorizes. Do not union linked alts' permissions.

## Base adapter and freshness

The pinned interface exposes `GetMapInstanceIdAsync(mapId)`, `IsEveMapperMapAccessAuthorized(characterId,mapId)` and `IsInstanceAdminAuthorized(characterId,instanceId)`. Use the per-map method, not the any-instance/global user handler. Null/unknown map-instance and wrong-map system deny. The inspected implementation consults character corporation/alliance data and local instance/map access; its existence alone does not establish current membership freshness.

Bridge contract `AccessDecision` contains actorId, mapId, instanceId, baseAllowed, moduleEpoch, baseEpoch, membershipObservedAt, membershipExpiresAt and evaluatedAt. Local module/base ACL changes invalidate affected decisions. No positive module authorization cache beyond one operation; every HTTP operation and each event recipient delivery obtains a fresh decision. Membership data may use the shared base HTTP cache only until its actual expiry and at most 300 seconds after observation. No new poller/early forced ESI refresh; if evidence of age/expiry cannot be supplied by the base client, the bridge must expose it as a maintained patch before live use. Unavailable/stale membership fails closed. Therefore external corporation changes have a stated maximum evidence age, not a false instantaneous detection promise.

Base ACL mutation, map removal/reparenting and account unlink/logout entry points must call bridge invalidation before acknowledging success. P0 has one app process; a shared per-map async read/write gate covers module authorization+commit/delivery and local base ACL mutation+epoch increment. Map writes/deletions take exclusive gate, module operations take shared gate; epoch is also persisted for restart safety. Character unlink/logout uses an equivalent per-character gate, acquired before the map gate; cross-map management locks increasing map IDs. No network await while holding a database transaction; fetch/cache membership evidence before acquiring gates, then verify it has not expired. If all base mutation seams cannot be covered, do not qualify the integrated release. Previously displayed or exported information cannot be remotely erased.

## Grants and operation rules

`Base` means verified session + current per-map base allowance + same-map references. Active means grant enabled, not expired, expected epoch valid. Explicit module grants are per character/map, never corporation-wide implicit grants. No module grant expands base access. `tools.annotate` does not imply `tools.view`; require both for contribution. `tools.manage` is an owner-only control, not assignable through the ordinary grant API. Hosting roles are separate.

| Operation | Capability | Contribution consent | Additional rule |
|---|---|---|---|
| TO-01 list/read | Base + tools.view | Not required | No deleted/expired text |
| TO-02 create manual note | Base + tools.view + tools.annotate | enabled and unexpired | Author server-derived |
| TO-03 edit own note | Base + tools.view + tools.annotate | enabled and unexpired | Author matches; expected revision; map/system immutable |
| TO-04 preview scan | Disabled in P0 | n/a | MODULE_OPERATION_UNAVAILABLE, no parser or persistence |
| TO-05 commit scan | Disabled in P0 | n/a | No base/sidecar writes |
| TO-06 route explanation | Disabled in P0 | n/a | Existing base route UI unaffected |
| TO-07 portable export | Disabled in P0 | n/a | No hidden bulk API |
| TO-08 change own contribution consent | Base + tools.view | Not required to disable/enable | Own character only; expected consent revision |
| TO-09 delete note | Base + tools.view + tools.annotate, or Base + tools.manage | Not required | Annotator deletes only own; manager any note; tombstone |
| TO-10 grant/revoke view/annotate | Base + tools.manage | Not required | Target verified, currently base-authorized on same map; manager cannot delegate manage |
| TE-01 subscribe/invalidation | Base + tools.view | Not required | Reauthorize before each delivery and every 30-second heartbeat |

Unknown operation/capability fails closed. P0 tools.review/tools.export cannot be granted. No HTTP route is registered for TO-04..07; tests of the bridge dispatcher return MODULE_OPERATION_UNAVAILABLE. A disabled whole module registers no product routes/events; unmatched HTTP is 404. Operational pairing is offline, not an anonymous web route.

## Consent meaning and retention

Consent controls **new personal contributions**, not reading other members' shared notes. Default is disabled, revision 0 (virtual absence). User enables for exactly the selected map with expiry between now+60 seconds and now+30 days. No silent renewal. At expiry or disable, reject create/edit and queued retries before idempotency result disclosure; stop any future collection mechanism. P0 has no automatic character observation collector. A non-sharing member with view grant can still read notes and delete their own notes under the rules above. Consent disable does not revoke CCP tokens or log out of WHMapper; UI states that explicitly.

Already saved notes remain shared until author/manager deletion or retention expiry: 90 days from last content edit, with a ten-minute stale badge independent of retention. Disabling sharing is prospective, not a misleading promise to retract all previous information. Confirm this text in the enable dialog. Access revocation instead blocks all module reads/writes/subscriptions on that map and clears app-private caches; logout/unlink also clears module session state. Remote token revocation errors do not prevent local shutdown. Disconnected/offline drafts cannot bypass the new decision after reconnect.

Retention is a selected P0 default, not legal advice: historical note text 30 days; deleted note text removed from primary storage in the same delete transaction; metadata-only audit/tombstone 90 days after event; rolling backups seven daily successful generations, maximum age seven days. Backups containing deleted text may persist within that period. Restores must apply the separately retained deletion/revocation journal before any public serving. Privacy removal uses the same authenticated deletion path or operator recovery path; no guarantee to erase information already copied by recipients. Changing these defaults is a versioned policy migration with revised tests.

## Owner pairing, transfer and loss

There is one module owner character per instance, persisted separately from grants. Owner powers still require current base instance administration and per-map base access. The deployment operator runs a local `pair-tools-owner` administrative command with explicit instanceId and characterId; verifies live `IsInstanceAdminAuthorized`, explicit operator confirmation, current verified login within ten minutes, and no existing owner. Serial transaction/unique instance constraint makes a second first-owner pairing fail. No empty-table self-claim route. CLI authenticates an operator OS/service identity and writes redacted audit, never reads a secret from chat.

Owner receives tools.manage on instance maps only where they also have base access; view/annotate are explicit ordinary grants. TO-10 assigns/revokes only view and annotate, expiry at most 30 days; no self-escalation or automatic grant on new map. Owner transfer is offline `transfer-tools-owner`, requiring operator confirmation, existing owner's verified approval within ten minutes, and target's current verified base instance-admin status. Atomic owner revision replaces old authority and invalidates sessions; no hosting power transfers.

If old owner is unavailable or loses base administration, the instance's management becomes locked; existing unexpired view/annotate grants remain subject to base access. Recovery is offline `recover-tools-owner`, maintenance mode, operator plus verified current base instance admin, written reason and evidence reference, explicit replacement confirmation. It increments ownership epoch, revokes all module grants and consent for the instance, disconnects module clients, then requires new explicit grants. Operator can stop the service/export encrypted recovery material but cannot claim invisible cryptographic isolation from their own host. Recovery tests must include no owner, duplicate pairing, stale approval, absent admin and lost owner. There is no automatic takeover timer.
