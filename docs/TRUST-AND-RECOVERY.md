# Roles, trust and recovery

## Proposed roles

| Role | Proposed authority |
| --- | --- |
| CEO | Appoint managers and recovery custodians; approve critical policy |
| Appointed manager | Manage explicitly delegated applications and assignments |
| Hardware owner | Offer resources, set limits, consent to workloads and revoke future hosting |
| Member | Use applications to which they are granted access |
| Recovery custodian | Retrieve or restore specifically authorised recovery material |

Deployment authority and permission to decrypt backups should be separate. CEO succession must not silently grant access to every historical secret. Exact rules remain a design decision.

## Hardware boundaries

Managers should only assign predefined approved workloads within an owner's offer. The design should avoid arbitrary remote commands and unrestricted access to the host operating system or personal files. Isolation does not make the physical host owner unable to inspect runtime data. Sensitive tokens and authoritative databases should therefore use appropriately trusted infrastructure.

## Backup and movement

A scheduled or clicked backup must produce a consistent recovery package, protect it in transit and at rest, verify integrity, and record completion or failure. Keys must be managed separately from encrypted copies. A successful upload is not proof of recoverability; a restore exercise is required.

A backup is not a live standby. An offline host cannot make a new backup. Recovery may lose changes since the most recent usable copy.

For a planned move: verify destination consent and compatibility; prepare the reviewed version; quiesce writes and jobs; capture or hand over consistent state; verify the destination; change routing; and fence the previous writer before admitting new writes. If verification fails, stop and use a tested rollback procedure. Never allow two authoritative writers merely because both hosts appear healthy.

Emergency recovery requires a prepared target and accessible recovery data. Automatic failover is a later capability requiring its own evidence.

Cloud networking, storage, scheduling and application hosting are separate responsibilities. Cloudflare was discussed as an optional access and backup component; it is not a complete deployment manager. Provider selection and current feature suitability remain unverified.
