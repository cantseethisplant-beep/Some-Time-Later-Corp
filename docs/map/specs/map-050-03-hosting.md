# Hosting module — proposed specification

Module ID `hosting`; independently versioned and disabled by default. It is optional for both WHMapper and WH Tools. Hosting the mapper on an Oracle VM does not require this module to be enabled.

## 1. Small first milestone

First deliver a host-offer and read-only health inventory, plus an explicit request/approval record. The controller may initially simulate fulfilment against fixtures. Production provisioning, billing, arbitrary workload execution, hardware-donor operation and destructive remote actions are not implied by that milestone.

The long-term intent remains affordable corporation hosting and explicitly offered hardware. Price, passive ISK income, CCP permissions, measured savings and supported application catalogue remain unverified decisions. No revenue scheme is enabled by this blueprint.

## 2. Separation and trust

The WHMapper module supplies authorized UI and a narrow request API. An optional separate controller holds provider adapters and remote management authority. No browser or module page receives OCI/Cloudflare keys, node credentials, shell access or a raw provider SDK handle. A base corporation map-admin grant is insufficient for host-operator operations.

The deployment operator and host owner may have access to plaintext workloads or secrets on their host. Encryption of a backup does not make an untrusted runtime operator unable to read live data. The approval record must state the host trust boundary and key custody. Never claim confidential computing or end-to-end protection absent an implemented, tested design.

The initial mapper backend may be registered as an **externally managed/read-only host**. The module cannot terminate, replace or remove the active controller/mapper/database host. Such maintenance requires a separate out-of-band runbook and explicit operator action.

## 3. Entities

| Entity | Required proposed fields and invariants |
|---|---|
| HostOffer | UUID id, instanceId integer, owner identity, capability labels/limits, region/architecture, trust statement, availability, consent version, revision; this is an offer, not an assignment |
| ManagedHost | UUID id, offer reference, enrollment identity, readOnly/externalManaged flags, last authenticated heartbeat, approved scopes; no anonymous endpoint self-enrollment |
| HostingRequest | UUID id, requestId UUID, idempotencyKey, instanceId, actor derived by server, hostOfferId, allowlisted operation, parameter schema, expected revision, requested expiry, state |
| Approval | UUID id, request/payload hash, approving host/operator identity, exact scopes/limits/expiry and revocation; approval of one payload cannot approve another |
| OperationReceipt | UUID id, request/approval refs, controller/adapter version, operation correlation, actual outcome/time, retry class, redacted diagnostics and rollback reference |
| RecoveryPolicy | UUID id, data scope, schedule/retention proposal, encryption/key-custody policy and target; backup artifact and restore exercise are separate linked records |

Host-offer consent, corporation scheduling choice and host-owner authorization are separate. Removing an offer stops new assignments, not an unsafe automatic deletion of active workloads.

## 4. Proposed operations and state transitions

| ID | Actor / operation | Expected behavior |
|---|---|---|
| HO-01 | hosting.viewer lists offers/health in its instance | redacted inventory, age and authentication state; no provider keys, other-tenant workload details or fake healthy default |
| HO-02 | verified host owner submits/changes offer | versioned capability/consent record; read-only until enrollment and explicit controller/operator approval |
| HO-03 | hosting.requester requests an allowlisted operation | validates exact parameter schema and host limits; produces a pending request, no immediate remote execution |
| HO-04 | host owner/operator approves/rejects | binds payload hash, scopes and expiry; self-approval rules explicit; corporation admin cannot bypass host owner |
| HO-05 | controller executes approved request | rechecks consent/ownership/approval/state, enforces quotas, writes idempotent receipt; provider timeout remains uncertain until reconciliation |
| HO-06 | authorized actor revokes/cancels | prevents future execution; in-flight uncertain results reconciled from actual provider state, not blindly replayed |
| HO-07 | operator plans backup/restore/update | separate approved lifecycle operation with evidence/rollback; restore exercise cannot be marked passed from backup creation |

Request states: draft → pending-approval → approved → executing → succeeded/failed/uncertain; cancellation/revocation/expiry can block execution. A retry may resume only a diagnosed retryable operation with the same immutable intent and an idempotent/provider reconciliation strategy. It cannot reuse a consumed approval to perform a second deployment or widen resources. Unsupported/destructive commands fail closed.

For the first release, permit only `inventory.read`, `health.read`, `request.record` and `approval.record`; real deployment adapters remain disabled until their own acceptance checks pass. Status text must distinguish simulated, pending, actual observed success and unknown outcome.

## 5. OCI / Cloudflare adapter boundary

Treat Oracle Always Free as an optional backend profile, not an assumption of perpetual available capacity. The initial profile records existing tenancy/region/shape/resource ceilings and a human-provisioned VM; the module does not upgrade an account, add a payment method, create paid shapes/storage or defeat idle-resource reclamation.

Cloudflare is the public midpoint. An optional adapter may manage precisely scoped hostnames/tunnel records only after approval; initial provisioning can remain manual. Do not place a broad Cloudflare API token in WHMapper UI. Tunnel credentials remain on the backend under operator custody and are independently rotatable. The app must still perform CCP SSO and tenant/module authorization; edge authentication alone is not a map permission decision.

The Oracle/Cloudflare option document gives the proposed network/data flow and qualification gates. Provider compatibility, account eligibility, free quota, region capacity, ARM64 images, backup destination and recovery are not established by a saved offer record.

## 6. Data, recovery and audit

The controller owns its database/schema; the module stores only the bounded request/projection it needs. Use authenticated, replay-resistant service requests with scoped identities, payload hashes, expiry and idempotency. The exact transport/key provisioning is an implementation decision to freeze before enabling execution; absent provisioning is a blocked state, never anonymous fallback.

A public map export excludes tokens/secrets. Full database/controller backups may contain private player/configuration data and must be treated as sensitive, encrypted under the documented operator key policy and kept outside Git/public object access. A durable off-host restore copy is required before relying on a reclaimable free VM. Key recovery and grant/identity preservation require a demonstrated isolated restore.

App/controller outage: the mapper remains available where its own dependencies are healthy; hosting operations show controller-unavailable and queue no hidden execution. Lost/revoked node: mark health unknown, stop new assignments and require explicit reconciliation. Audit records contain identity, payload/approval hash, requested versus actual effect and evidence status, with redacted errors—not credentials or raw debug dumps.

## 7. Disable and upgrade

With Hosting disabled there are no hosting routes/events/controller calls. Module upgrades do not mutate base map ownership or force WH Tools upgrades unless the compatibility manifest says so. Database migrations are module-owned, backed up and tested with rollback/forward-recovery plans. Disabling the module never deletes live remote workloads.
