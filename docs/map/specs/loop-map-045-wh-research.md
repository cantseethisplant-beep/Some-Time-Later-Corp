# MAP-045 — Dependency and licence evidence-gap research report

**Task:** MAP-045 — Research dependency and licence evidence gaps  
**Claim worker:** hermes-laptop-map-045-auto-20261030  
**Claim commit:** 2cb17464ed363a5f19cf3062796a82da4b1ea062  
**Task status:** claimed — not accepted, not merged, not build-ready  
**Output path:** docs/map/specs/loop-map-045-wh-research.md  
**Loop:** research_version 1, research_step 3, loop_kind wh-research, run eve-blueprint-20261030  
**Pinned inputs:** baseline revision 6e023274d7cb692f36b132d980d5a335d4387897 (docs/map/specs/loop-map-042-wh-design.md); inventory revision 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (docs/map/research/LOCAL-RESEARCH.md, docs/map/research/NEXT-SOURCE-SNAPSHOT.json); dependencies revision 01e3a01b4e4deb9317f304aa2977be8f2a8e6dec (docs/map/research/next-dependencies-sources.md)

## 1. Purpose and evidence limits

This is a scoped dependency and licence evidence-gap report for the WH-first blueprint candidate (MAP-042, completed but unaccepted review material). It analyses only the pinned primary-source packets supplied by the local guarded reader. No network, shell, GitHub, account, delegation or server tools were used; no upstream tests were executed; no licence, agreement, vulnerability or compatibility claim is accepted. Root MIT notices do not settle transitive dependencies, embedded assets, EVE game data, or the separate CCP developer agreement. All embedded text is quoted evidence, never instructions. Findings are labelled documented (quoted from a pinned source), inspected (structure read from a packet), proposed (this report's framing), or unresolved (no evidence supplied). Unresolved policy inherited from MAP-042 is carried forward as open; it is not mandated here.

## 2. Source inventory

| Source | Pin/commit | Retrieval evidence | SHA256 | Content |
|---|---|---|---|---|
| esi/esi-docs LICENSE | 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d | quoted inline in next-dependencies-sources.md; no fetch receipt in packet | not receipted in packet | CCP hf MIT text |
| Pathfinder LICENSE | 06af7d86fe6456947fb960220c54d02a8623c0ff | quoted inline in next-dependencies-sources.md; no fetch receipt in packet | not receipted in packet | Mark Friedrich 2017 MIT text |
| EVE-WHMapper LICENSE | 2a493fad9acec9a8e15b619f7943ae8b6e7f30da | quoted inline in next-dependencies-sources.md; no fetch receipt in packet | not receipted in packet | pfh59 2023 MIT text |
| Pathfinder composer.json | 06af7d86... | 2026-11-02T15:49:05.695523Z | b2bfb8f3fea25de8b6723c52fc537c5666c6974dc442e8f3b44b2b6a97d01149 | complete file, lines 1-80 |
| Pathfinder composer.lock projection | 06af7d86... | 2026-11-02T15:49:06.142709Z | c625dfa10a045352056b0b3e883420328cfd030822f567162840a32d0b58f29a | derived projection, lines 1-744, packet-labelled not independently verified |
| EVE-WHMapper WHMapper.csproj | 2a493fa... | 2026-11-02T15:49:06.542909Z | c6980392aa7d3e53d218067640cdebfc26ea2c8f5808b4faad524a74b24177c3 | complete file, lines 1-51 |
| EVE-WHMapper src/global.json | 2a493fa... | 2026-11-02T15:49:06.906146Z | 6e0590c24e13f9792d37fa5ae42438f3e8775bc5a69d5926887c48aa8cab639a | complete file, lines 1-6 |
| esi/esi-docs docs/resources/license.md | 98b42d5... | 2026-11-02T15:49:07.347027Z | 1a8569cfce680a5c9cf1687184443db8d78ec722771709f00c997f2f41f8aae6 | developer agreement pointer, lines 1-3 |

Receipts establish what was fetched, not that any implementation works.

## 3. Findings

### 3.1 Pathfinder composer.json — declared manifest (documented)

Pinned commit 06af7d86..., complete file supplied. Declared `license`: MIT; `config.lock`: true. PHP platform requirement `php-64bit >=8.2`; extensions `ext-pdo`, `ext-openssl`, `ext-curl`, `ext-json`, `ext-mbstring`, `ext-ctype`, `ext-gd`, `ext-sodium` all declared `"*"` (floating, no upper bound); `ext-redis` appears only in `suggest`, i.e. optional, not required.

Production `require` mixes exact and floating declarations:
- Exact: `goryn-clade/pathfinder_esi 3.0.2-beta.2`
- Floating/ranges: `bcosca/fatfree-core 3.9.*`, `ikkez/f3-cortex dev-master#47d2596914776877ef4d87706d1faa812d1398f2` (floating branch plus commit suffix), `ikkez/f3-sheet 0.4.*`, `xfra35/f3-cron 1.3.*`, `monolog/monolog ^3`, `league/html-to-markdown 5.2.*`, `cache/redis-adapter ^1.2`, `cache/array-adapter 1.1.*`, `cache/void-adapter ^1.1`, `cache/namespaced-cache 1.1.*`, `react/promise ^3.2`, `react/socket ^1.16`, `react/promise-stream ^1.7`, `clue/ndjson-react ^1.3`, `firebase/php-jwt ^7`

Risk-relevant config (documented observations, no vulnerability claimed):
- `config.audit.ignore`: `["PKSA-y2cr-5h3j-g3ys"]` — one audit-ignore entry needing owner review.
- `config.allow-plugins`: `{"dealerdirect/phpcodesniffer-composer-installer": true}` — plugin execution permitted.
- `repositories`: one VCS repository for `goryn-clade/pathfinder_esi`.

Dev tooling is cleanly separated in `require-dev`: `phpstan/phpstan ^2.3`, `squizlabs/php_codesniffer ^4.0`, `phpcompatibility/php-compatibility ^10.0@alpha`, `rector/rector ^2.7`, `phpstan/phpstan-deprecation-rules ^2.0`, with `phpstan`, `phpcs`, `rector` scripts.

### 3.2 Pathfinder composer.lock projection — locked versions (inspected, unverified)

Supplied lines 1-744; the packet labels this a derived projection, "not independently verified dependency licences or vulnerability audit". Locked exact versions observed:

Direct production packages declared in composer.json `require`, with locked versions from the projection:
- `bcosca/fatfree-core 3.9.*` → locked 3.9.3 (GPL-3.0)
- `ikkez/f3-cortex dev-master#47d2596914776877ef4d87706d1faa812d1398f2` → dev-master (GPL-3.0)
- `ikkez/f3-sheet 0.4.*` → v0.4.3 (GPL-3.0)
- `xfra35/f3-cron 1.3.*` → v1.3.0 (GPL-3.0-only)
- `league/html-to-markdown 5.2.*` → 5.2.3 (MIT)
- `monolog/monolog ^3` → 3.12.1 (MIT)
- `cache/redis-adapter ^1.2` → 1.2.0 (MIT)
- `cache/array-adapter 1.1.*` → 1.1.0 (MIT)
- `cache/void-adapter ^1.1` → 1.2.0 (MIT)
- `cache/namespaced-cache 1.1.*` → 1.1.0 (MIT)
- `react/promise ^3.2` → v3.3.0 (MIT)
- `react/socket ^1.16` → v1.17.0 (MIT)
- `react/promise-stream ^1.7` → v1.7.0 (MIT)
- `clue/ndjson-react ^1.3` → v1.3.0 (MIT)
- `goryn-clade/pathfinder_esi 3.0.2-beta.2` → v3.0.2-beta.2 (MIT)
- `firebase/php-jwt ^7` → v7.2.1 (BSD-3-Clause)

These root-require packages are direct production dependencies even where the lock projection also resolves them transitively.

Transitive (inferred; no require-tree graph supplied):
- `cache/adapter-common 1.3.0` (MIT), `cache/hierarchical-cache 1.2.0` (MIT), `cache/tag-interop 1.1.0` (MIT)
- `guzzlehttp/guzzle 7.15.5` (MIT), `guzzlehttp/promises 2.5.3` (MIT), `guzzlehttp/psr7 2.13.1` (MIT)
- `react/cache v1.2.0`, `react/dns v1.14.0`, `react/event-loop v1.6.0`, `react/stream v1.4.0` (MIT)
- `caseyamcl/guzzle_retry_middleware v2.13.0` (MIT), `evenement/evenement v3.0.2` (MIT), `ralouphie/getallheaders 3.0.3` (MIT)
- `psr/*` and `symfony/*` packages (MIT)
- `ikkez/f3-schema-builder v2.2.6` (GPL-3.0), requiring `bcosca/fatfree-core ^3.6`

Dev-only: `phpstan/phpstan 2.3.1` (MIT), `phpstan/phpstan-deprecation-rules 2.0.5` (MIT), `rector/rector 2.7.0` (MIT), `squizlabs/php_codesniffer 4.0.4` (BSD-3-Clause), `phpcompatibility/php-compatibility 10.0.0-alpha2` (LGPL-3.0-or-later), `phpcsstandards/phpcsutils 1.2.3` (LGPL-3.0-or-later). `dealerdirect/phpcodesniffer-composer-installer v1.2.1` (MIT) appears as an allow-plugin entry and is dev-associated.

Declared SPDX labels inside the projection are not inspected licence files. Direct vs transitive cannot be fully separated from the projection alone; composer.json `require` entries are the authoritative direct declarations.

### 3.3 EVE-WHMapper WHMapper.csproj — .NET manifest (documented)

Pinned commit 2a493fa..., complete file supplied. `TargetFramework net10.0`; `src/global.json` pins SDK `10.0.100` with `rollForward latestMinor`. All dependencies are `PackageReference` entries; no `packages.lock.json` or equivalent lock file was supplied, so locked .NET versions are unavailable — declarations only.

Exact declarations: `Microsoft.Extensions.Http.Resilience 10.9.0`, `MudBlazor 9.9.0`, `Serilog.Sinks.File 7.0.0`, `Z.Blazor.Diagrams 3.0.4.1`, `Z.Blazor.Diagrams.Algorithms 3.0.4.1`, `FibonacciHeap 2.0.2`, `Microsoft.IdentityModel.Protocols.OpenIdConnect 8.22.0`, `Microsoft.IdentityModel.JsonWebTokens 8.22.0`, OpenTelemetry set `1.18.0` including `OpenTelemetry.Instrumentation.Process 1.18.0-rc.1` (pre-release).

Floating/wildcard declarations: `Microsoft.EntityFrameworkCore 10.*`, `Serilog.AspNetCore 10.*`, `Serilog.Settings.Configuration 10.*`, `YamlDotNet 18.*`, `FluentValidation 12.*`, `Microsoft.AspNetCore.SignalR.Client 10.*`, `Microsoft.AspNetCore.Authentication.JwtBearer 10.*`, `Npgsql 10.*`, `Npgsql.EntityFrameworkCore.PostgreSQL 10.*`, `Microsoft.AspNetCore.Authentication.OpenIdConnect 10.*`, `Microsoft.EntityFrameworkCore.Design 10.*` (design-time), `Microsoft.Extensions.Caching.StackExchangeRedis 10.*`, `Microsoft.AspNetCore.DataProtection.StackExchangeRedis 10.*`.

No separate dev manifest was supplied, so production/dev separation for .NET is not evidenced by this packet. Embedded asset `Resources/wh-effects.json` is included as `EmbeddedResource`; its licence is unverified and is not covered by the root MIT.

### 3.4 esi/esi-docs — documentation licence and CCP developer agreement (documented)

`docs/resources/license.md` states the developer license agreement must be signed before creating third-party applications and links `/license-agreement`; the official agreement is `https://developers.eveonline.com/license-agreement`. The esi/esi-docs LICENSE is MIT, Copyright © 2015 CCP hf, covering that docs repository only. Status: agreement linked but unsigned; no commercial/ISK model approved; no EVE game-data or ESI terms evidence beyond this pointer.

### 3.5 Root licence separation (proposed framing)

Documented root MIT notices: esi/esi-docs (CCP hf, 2015), Pathfinder (Mark Friedrich, 2017), EVE-WHMapper (pfh59, 2023). Each covers its own repository. None settles: Pathfinder's GPL-3.0/BSD-3/LGPL transitive stack; EVE-WHMapper's unknown NuGet tree; embedded assets (Pathfinder favicon/logo, EVE-WHMapper wh-effects.json); EVE game data; ESI terms of use; the separate CCP developer agreement. Owner legal interpretation and revenue approval remain unresolved.

## 4. Scoped inventory (not a complete SBOM)

| Package | Manifest | Declaration | Locked | Declared licence | Group | Direct/transitive | Notes |
|---|---|---|---|---|---|---|---|
| bcosca/fatfree-core | composer.json + lock | 3.9.* | 3.9.3 | GPL-3.0 | prod | direct | GPL in prod stack |
| goryn-clade/pathfinder_esi | composer.json + lock | 3.0.2-beta.2 | v3.0.2-beta.2 | MIT | prod | direct | VCS repository also declared |
| firebase/php-jwt | composer.json + lock | ^7 | v7.2.1 | BSD-3-Clause | prod | direct | |
| monolog/monolog | composer.json + lock | ^3 | 3.12.1 | MIT | prod | direct | |
| league/html-to-markdown | composer.json + lock | 5.2.* | 5.2.3 | MIT | prod | direct | |
| ikkez/f3-cortex | composer.json + lock | dev-master#47d2596914776877ef4d87706d1faa812d1398f2 | dev-master | GPL-3.0 | prod | direct | floating branch |
| ikkez/f3-sheet | composer.json + lock | 0.4.* | v0.4.3 | GPL-3.0 | prod | direct | |
| xfra35/f3-cron | composer.json + lock | 1.3.* | v1.3.0 | GPL-3.0-only | prod | direct | |
| cache/redis-adapter | composer.json + lock | ^1.2 | 1.2.0 | MIT | prod | direct | declared directly in require |
| cache/array-adapter | composer.json + lock | 1.1.* | 1.1.0 | MIT | prod | direct | declared directly in require |
| cache/void-adapter | composer.json + lock | ^1.1 | 1.2.0 | MIT | prod | direct | declared directly in require |
| cache/namespaced-cache | composer.json + lock | 1.1.* | 1.1.0 | MIT | prod | direct | declared directly in require |
| react/promise | composer.json + lock | ^3.2 | v3.3.0 | MIT | prod | direct | declared directly in require |
| react/socket | composer.json + lock | ^1.16 | v1.17.0 | MIT | prod | direct | declared directly in require |
| react/promise-stream | composer.json + lock | ^1.7 | v1.7.0 | MIT | prod | direct | declared directly in require |
| clue/ndjson-react | composer.json + lock | ^1.3 | v1.3.0 | MIT | prod | direct | declared directly in require |
| guzzlehttp/guzzle | composer.json (via dep) + lock | ^7.0 via dep | 7.15.5 | MIT | prod | transitive | inferred |
| cache/adapter-common | lock | — | 1.3.0 | MIT | prod | transitive | via cache adapters |
| cache/hierarchical-cache | lock | — | 1.2.0 | MIT | prod | transitive | |
| cache/tag-interop | lock | — | 1.1.0 | MIT | prod | transitive | |
| ikkez/f3-schema-builder | lock | — | v2.2.6 | GPL-3.0 | prod | transitive | requires fatfree-core ^3.6 |
| dealerdirect/phpcodesniffer-composer-installer | config.allow-plugins + lock | true | v1.2.1 | MIT | dev | plugin | allow-plugin entry |
| phpstan/phpstan | require-dev + lock | ^2.3 | 2.3.1 | MIT | dev | direct | |
| squizlabs/php_codesniffer | require-dev + lock | ^4.0 | 4.0.4 | BSD-3-Clause | dev | direct | |
| phpcompatibility/php-compatibility | require-dev + lock | ^10.0@alpha | 10.0.0-alpha2 | LGPL-3.0-or-later | dev | direct | |
| phpstan/phpstan-deprecation-rules | require-dev + lock | ^2.0 | 2.0.5 | MIT | dev | direct | |
| rector/rector | require-dev + lock | ^2.7 | 2.7.0 | MIT | dev | direct | |
| phpcsstandards/phpcsutils | require-dev + lock | — | 1.2.3 | LGPL-3.0-or-later | dev | transitive (dev) | |
| Microsoft.EntityFrameworkCore | WHMapper.csproj | 10.* | not supplied | not inspected | prod | direct | no .NET lock |
| Npgsql | WHMapper.csproj | 10.* | not supplied | not inspected | prod | direct | |
| MudBlazor | WHMapper.csproj | 9.9.0 | not supplied | not inspected | prod | direct | |
| OpenTelemetry.Instrumentation.Process | WHMapper.csproj | 1.18.0-rc.1 | not supplied | not inspected | prod | direct | pre-release |

Remaining lock-projection entries (react/*, psr/*, symfony/*, evenement, ralouphie/getallheaders, caseyamcl/guzzle_retry_middleware, other react packages) are documented in §3.2 but abbreviated here. This is a scoped inventory, not a complete SBOM.

## 5. Risks identified without vulnerability claims

- `composer.json config.audit.ignore` names `PKSA-y2cr-5h3j-g3ys`: an audit-ignore entry requiring owner review; this packet asserts no advisory or vulnerability.
- `config.allow-plugins` permits `dealerdirect/phpcodesniffer-composer-installer`: plugin-execution risk requiring review.
- Floating declarations (`3.9.*`, `^3`, `dev-master`, `10.*`, `18.*`) allow resolved versions to change between installs; composer.lock pins Pathfinder but is an unverified projection here.
- `dev-master#<commit>` for ikkez/f3-cortex is a floating branch, not an immutable release.
- `OpenTelemetry.Instrumentation.Process 1.18.0-rc.1` is a declared pre-release.
- .NET: no lock file; `10.*`/`12.*`/`18.*` ranges unresolved; transitive tree unknown.
- Declared SPDX labels inside the lock are not inspected licence files.
- GPL-3.0-family entries appear in the production Pathfinder stack (fatfree-core, f3-cortex, f3-sheet, f3-cron, and transitive f3-schema-builder); root MIT does not clear these.

## 6. Exact remaining upstream checks

1. Pathfinder: inspect actual licence files (not lock labels) for the GPL-3.0 family and BSD-3-Clause firebase/php-jwt; verify composer.lock hash consistency against the repository.
2. Pathfinder: owner review of `config.audit.ignore` entry PKSA-y2cr-5h3j-g3ys and `config.allow-plugins` entry.
3. EVE-WHMapper: obtain packages.lock.json or equivalent; inspect declared and transitive NuGet licences; confirm acceptability of `10.*` ranges.
4. Assets: Pathfinder favicon/logo; EVE-WHMapper wh-effects.json — locate and read licence files.
5. EVE: read the CCP developer agreement at https://developers.eveonline.com/license-agreement; owner legal review; revenue/ISK model remains unresolved.
6. ESI scopes, rate limits and issuer contract: see sibling research packets (next-esi-sources.md / next-auth-sources.md), not supplied in this task's inputs.
7. Owner decisions: stack/runtime (OD-02), dependency audit scope (OD-04), asset and game-data licences (OD-05), database engine (OD-12) — none resolved by this packet.

## 7. Checks performed vs not performed

Performed (document-level only): read pinned composer.json, composer.lock projection, WHMapper.csproj, global.json, three root LICENSE texts and esi license.md; separated declared vs locked versions (PHP locked via unverified projection; .NET declarations only, no lock supplied); separated `require` from `require-dev` for PHP; identified prod versus design-time declarations for .NET where identifiable; catalogued audit-ignore and allow-plugin entries; catalogued declared GPL-3.0/BSD-3-Clause/MIT/LGPL labels in the projection; verified root-require packages against composer.json for direct-vs-transitive classification.

Not performed: composer install or audit, `dotnet restore` or vulnerability scan, licence-file inspection beyond the three root LICENSE texts, SBOM generation, asset licence reads, CCP agreement review, any legal interpretation, compatibility test, security test, or runtime behaviour test.

## 8. Unresolved owner decisions (precise)

- OD-02 target language/runtime/stack: PHP Pathfinder vs .NET EVE-WHMapper vs new implementation — blocks dependency acceptance.
- OD-04 full dependency licence/security audit for both manifests including audit-ignore review — missing.
- OD-05 asset licence check (wh-effects.json, Pathfinder favicon/logo) and EVE game-data/ESI terms — unchecked.
- OD-12 database engine undecided; the MAP-042 docker-compose Postgres reference is example only.

These OD references carry forward MAP-042 section 15 decisions as proposals/open owner decisions; they are not adopted mandates in this report.

This report proposes nothing for acceptance, merge, deployment or certification as build-ready.
