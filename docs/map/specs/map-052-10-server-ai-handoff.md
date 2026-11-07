# Server-AI intake and continuation contract

Owner direction, 7 November 2026: the server AIs are the future builders. The laptop is a documentation/handoff workspace. This package prepares their work; no connection, execution, software installation or agent launch on either host is performed by preparing it.

## Three distinct machines/roles

| Role | Responsibility | Required evidence |
|---|---|---|
| Build executor | Server AI workspaces, source/dependency resolution, isolated fixtures, tests, review artifacts | Observed identity/architecture/tooling, selected-repo access, available capacity and isolated workspace |
| Production origin | Later qualified WHMapper/Tools deployment behind Cloudflare; Oracle remains an option | Actual quota/capacity/architecture/domain/proxy/SSO/recovery qualification |
| Recovery destination | Encrypted off-origin backup and append-only privacy-decision journal | Independent failure domain, durable receiver/keys/export/retention, custody and restore evidence |

One physical host may fill build+recovery roles only after checking capacity/isolation, and only when the runtime origin is elsewhere. A co-located VM/container/directory on the origin does not meet off-origin recovery. No role requires an online laptop. No private server hostname/IP, credential, GPU capacity or installed agent stack is assumed from old conversation history.

## Portable source intake

Read `manifest.json` and verify its files' SHA-256 before using the ZIP. In GitHub, use the exact MAP-052 output commit recorded in the public guide/manifest, not a moving PR head. The pinned upstream remains `pfh59/eve-whmapper@2a493fad9acec9a8e15b619f7943ae8b6e7f30da`. V4 is the current contract; v3 files/reports are historical evidence within their original scope. Do not concatenate conflicting generations into one prompt.

Future implementation belongs in private `cantseethisplant-beep/Eve-Cloud`; public `Some-Time-Later-Corp` holds planning, safe progress and MAP claims. Server credentials are provisioned through its existing authorised credential mechanism for selected repos only. Never copy laptop `.dpapi` files, `.env`, Windows runtime paths, browser cookies, old worker RUN.json, usage SQLite, claim tokens or `local_github.py` into the server as a bootstrap shortcut. The old free-only Hermes counter is historical 255/800, not a newly granted server quota. A free inference route/model and account budget must be checked locally by the server operator before enabling model work; no paid fallback or assumed free model identity is authorised here.

The Python scripts archived with earlier handoffs are coordinator publication/contract utilities, not a Linux launcher or app. Server workers can consume the JSON Schema and fixture files without importing a Windows coordinator. Native runtime/skills are observed on the server before use; do not install or select tools merely because they existed on the laptop.

## Intake preflight — observe, do not build

Create one private receipt `evidence/intake/<UTC>-server-preflight.json`. Record observedAt, actor identity, host identity, OS/architecture, workspace, source manifest digest, public/private repository accessibility, SDK/compiler versions, container engine/daemon availability or separately approved isolated DB alternative, disk availability and selected agent runtime version. Every field has observed/unavailable/not_checked status, evidence path and reason. Do not dump environment variables, authentication output, secrets or unrelated host inventory. These values are supplied by read-only observations, never populated with example hostnames.

Possible Linux probes, run only during an authorised server intake, in a private workspace:

```sh
id -un
hostname
pwd
uname -srm
if command -v dotnet >/dev/null 2>&1; then dotnet --list-sdks; else echo 'SDK probe unavailable'; fi
if command -v git >/dev/null 2>&1; then git --version; else echo 'Git unavailable'; fi
if command -v docker >/dev/null 2>&1; then docker version --format '{{.Client.Version}} / {{if .Server}}{{.Server.Version}}{{end}}'; else echo 'Docker unavailable'; fi
df -Pk .
```

These are suggested observations, not a statement that Linux/Docker is installed. A failed daemon probe is a failed/unavailable observation, not permission to start services or add the AI to privileged groups. Use the server's supported equivalent for another platform; record the change. An SDK/container installation or permission change is a separate concrete remediation task under server authority. Laptop SDK/Docker status is irrelevant.

## Review, build and release gates

1. Independent reviewer checks this specification and gap register against the pinned source. Author cannot accept its own output. Return exact findings with affected paths and severity, or an explicit scoped approval. A generic “looks good” is insufficient evidence of runtime success.
2. Coordinator admits only ready tasks whose immutable inputs are present and accepted under that task's declared mode. Review tasks may inspect completed unaccepted drafts for review, not treat them as accepted build requirements. See 12 for the planned queue; it is not an installed scheduler.
3. After build authority and specification acceptance are recorded, begin isolated upstream baseline, then bridge, then notes. Use synthetic SSO/ESI identities and private databases. No production tokens, Cloudflare tunnel, cloud provisioning or live corporation data in the baseline.
4. A verifier records exact command/result/artifact/input hashes; reviewer accepts/rejects the task. Unfinished or rejected output cannot satisfy another ready task's dependency. Every component result states OS/architecture: x64 success is not an ARM64 runtime pass.
5. Live policy/custody/domain/account decisions and Q runtime checks govern later release. Build permission is not publication, paid inference, infrastructure purchase or production deployment permission.

## Copy/paste intake prompt

> Prepare intake for the Some Time Later Corp / Eve-Cloud WHMapper project using the v4 manifest and docs 00..12 at their immutable published revision. Read 10, 11 and 12 first, then the contract documents. The server is the future build executor; the laptop has no required build/runtime/recovery role. Verify package hashes and perform only read-only source/environment intake under your existing server permissions. Do not provision, install, build, change credentials or launch implementation workers during intake. Keep source facts, proposed design defaults, independent acceptance and runtime observations distinct. Produce a private preflight receipt, a focused independent review with source/contract references, and the next eligible task plus exact blockers. Use selected repositories only; keep credentials and raw logs private. No paid model fallback, quota reset, repeated broad audit or consumption of unfinished work. Follow the queue's atomic one-task claim protocol before any admitted production task. Return durable paths/commit hashes and one resumable checkpoint; do not claim an app was built or deployed from this prompt.

## Resume/checkpoint and stopping

Private `handoff/CURRENT.md` records manifest/commit, active task/claim generation, last durable effect, result/check status, next exact step, blockers and evidence index path. It contains no credentials. A worker checks it and the current authoritative claim after restart; old ownership is not restored by a log line. Coordinator stops on exhausted budget, owner STOP, missing supervisor for an autonomous run, revoked claim/access, unresolved unsafe input or no eligible queue. It saves artifacts and releases only its own claim. It does not widen scope or generate indefinite audit tasks to stay busy. The user requests progress by asking the server coordinator to read this checkpoint; the laptop/chat does not need to remain open.
