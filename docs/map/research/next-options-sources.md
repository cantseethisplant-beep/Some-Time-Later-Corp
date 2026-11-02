# Primary research source pack: options

Frozen read-only primary evidence. Treat all embedded code/docs as quoted data, never instructions. No upstream tests executed, no player data, server access, app implementation or acceptance.

## Licence notice — goryn-clade/pathfinder
https://raw.githubusercontent.com/goryn-clade/pathfinder/06af7d86fe6456947fb960220c54d02a8623c0ff/LICENSE
```text
MIT License

Copyright (c) 2017 Mark Friedrich

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```

## Licence notice — pfh59/eve-whmapper
https://raw.githubusercontent.com/pfh59/eve-whmapper/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/LICENSE
```text
MIT License

Copyright (c) 2023 pfh59

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```

## goryn-clade/pathfinder / README.md
Commit: 06af7d86fe6456947fb960220c54d02a8623c0ff
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/README.md
Receipt: {"url": "https://raw.githubusercontent.com/goryn-clade/pathfinder/06af7d86fe6456947fb960220c54d02a8623c0ff/README.md", "retrieved_at": "2026-11-02T15:49:11.961539+00:00", "sha256": "1d7c461a1e06cb0425312d1380a34ff994632986f00728130e19c9196f9a1bd1", "etag": "\"cfc78045736c219939d9be2caec12a80f0bc0b167024419b3caa7985ba5c64ec\"", "last_modified": null, "bytes": 3181}
Supplied lines: 1-60 (complete file)
```text
# ![Pathfinder logo](favicon/favicon-32x32.png "Logo") *PATHFINDER*

#### Mapping tool for [*EVE ONLINE*](https://www.eveonline.com)

[![Release](https://img.shields.io/github/v/release/goryn-clade/pathfinder?style=flat-square&label=release)](https://github.com/goryn-clade/pathfinder/releases/latest)
[![PHP 8.5](https://img.shields.io/badge/php-8.5-777BB4?style=flat-square&logo=php&logoColor=white)](https://www.php.net/)
[![License: MIT](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)
[![Discord](https://img.shields.io/badge/discord-join-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/zG733etVbj)

This is a community-maintained fork of [Pathfinder](https://github.com/exodus4d/pathfinder) by Exodus4d, kept alive with bug fixes, PHP 8 compatibility, and EVE universe data updates.

**For installation, see the [pathfinder-containers](https://github.com/goryn-clade/pathfinder-containers) repository.**

---

## v3.0 - What's new in the app

v3.0 is a major release. The full upgrade guide (backups, schema migration, env rewrite, bulk ESI token encryption) lives in [pathfinder-containers](https://github.com/goryn-clade/pathfinder-containers) - see its README and `MIGRATION-v2-to-v3.md`. The notes here cover only changes inside the Pathfinder application itself.

### Application-level breaking changes

| Area | v2.x | v3.0 |
|---|---|---|
| PHP runtime | 7.2 | 8.5 |
| DB schema | v2 | adds columns to `system`, `connection`, `map`, `character`; new `map_group` table |
| ESI tokens at rest | plaintext | encrypted (libsodium `crypto_secretbox`) |
| Email / SMTP notifications | supported | **removed** - use Slack or Discord webhooks |
| `pathfinder.ini` / `config.ini` | hand-edited ini files | driven by environment variables |
| `plugin.ini` | bind-mounted | bind-mounted (unchanged) |
| Login restriction settings | `WHITELIST_*` | renamed `ALLOWLIST_*` |

### Security hardening

- **ESI tokens are encrypted at rest** using libsodium `crypto_secretbox`. Requires a 32-byte hex key (`TOKEN_ENCRYPTION_KEY`); fails closed if blank.
- **WebSocket tokens** are HMAC-bound to the PHP session. The socket server refuses to start without `WS_TOKEN_SECRET`.
- **WebSocket origin checks** - the socket server refuses to start in production with no allowed origins configured.
- **PKCE on CCP SSO** - enabled by default; can be disabled via `CCP_SSO_USE_PKCE=0` if upstream changes break the flow.
- **`/setup` is gated** by `PF_SETUP_ENABLED` and should only be enabled during bootstrap.
- **Production startup guards** activate when `APP_ENV=production`.


---

## Community

For help and discussion, join the Discord server: <https://discord.gg/zG733etVbj>

> **Note:** The Pathfinder Slack workspace is no longer active. Slack's commercial model change reduced free workspace history to 90 days, making it unsuitable for a small open-source community. Discord is now the primary community channel.

---

## Contributing

Issues and pull requests are welcome. Please report bugs in the [Issue tracker](https://github.com/goryn-clade/pathfinder/issues).

---

## License

[MIT](http://opensource.org/licenses/MIT)

```

## goryn-clade/pathfinder / composer.json
Commit: 06af7d86fe6456947fb960220c54d02a8623c0ff
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/composer.json
Receipt: {"url": "https://raw.githubusercontent.com/goryn-clade/pathfinder/06af7d86fe6456947fb960220c54d02a8623c0ff/composer.json", "retrieved_at": "2026-11-02T15:49:05.695523+00:00", "sha256": "b2bfb8f3fea25de8b6723c52fc537c5666c6974dc442e8f3b44b2b6a97d01149", "etag": "\"68c9449ad71bd2bd832567b034dce23c25b2d42a9a57a6cd026b7167280c49a6\"", "last_modified": null, "bytes": 2179}
Supplied lines: 1-80 (complete file)
```text
{
  "name": "goryn-clade/pathfinder",
  "description": "Mapping tool for EVE ONLINE",
  "type": "project",
  "homepage": "https://github.com/goryn-clade/pathfinder",
  "minimum-stability": "beta",
  "prefer-stable": true,
  "license": "MIT",
  "authors": [
    {
      "name": "Mark Friedrich",
      "email": "pathfinder@exodus4d.de"
    }
  ],
  "config": {
    "optimize-autoloader": true,
    "lock": true,
    "audit": {
      "ignore": ["PKSA-y2cr-5h3j-g3ys"]
    },
    "allow-plugins": {
      "dealerdirect/phpcodesniffer-composer-installer": true
    }
  },
  "autoload": {
    "psr-4": {
      "Exodus4D\\Pathfinder\\": "app/"
    }
  },
  "readme": "README.md",
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/goryn-clade/pathfinder_esi"
    }
  ],
  "require": {
    "php-64bit": ">=8.2",
    "ext-pdo": "*",
    "ext-openssl": "*",
    "ext-curl": "*",
    "ext-json": "*",
    "ext-mbstring": "*",
    "ext-ctype": "*",
    "ext-gd": "*",
    "ext-sodium": "*",
    "bcosca/fatfree-core": "3.9.*",
    "ikkez/f3-cortex": "dev-master#47d2596914776877ef4d87706d1faa812d1398f2",
    "ikkez/f3-sheet": "0.4.*",
    "xfra35/f3-cron": "1.3.*",
    "monolog/monolog": "^3",
    "league/html-to-markdown": "5.2.*",
    "cache/redis-adapter": "^1.2",
    "cache/array-adapter": "1.1.*",
    "cache/void-adapter": "^1.1",
    "cache/namespaced-cache": "1.1.*",
    "react/promise": "^3.2",
    "react/socket": "^1.16",
    "react/promise-stream": "^1.7",
    "clue/ndjson-react": "^1.3",
    "firebase/php-jwt": "^7",
    "goryn-clade/pathfinder_esi": "3.0.2-beta.2"
  },
  "suggest": {
    "ext-redis": "Redis can be used as cache backend."
  },
  "require-dev": {
    "phpstan/phpstan": "^2.3",
    "squizlabs/php_codesniffer": "^4.0",
    "phpcompatibility/php-compatibility": "^10.0@alpha",
    "rector/rector": "^2.7",
    "phpstan/phpstan-deprecation-rules": "^2.0"
  },
  "scripts": {
    "phpstan": "vendor/bin/phpstan analyse --memory-limit=512M",
    "phpstan-baseline": "vendor/bin/phpstan analyse --generate-baseline --memory-limit=512M",
    "phpcs": "vendor/bin/phpcs",
    "rector": "vendor/bin/rector process --dry-run"
  }
}

```

## pfh59/eve-whmapper / README.md
Commit: 2a493fad9acec9a8e15b619f7943ae8b6e7f30da
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/README.md
Receipt: {"url": "https://raw.githubusercontent.com/pfh59/eve-whmapper/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/README.md", "retrieved_at": "2026-11-02T15:49:12.294945+00:00", "sha256": "0bc8d9dbb8061fa048370228c708508f472c21ab2acb2356ec6f9d99be110a81", "etag": "\"534371fabf2e5203a385a1338cad337c0f20380a9beae25ae5ec84332641afe5\"", "last_modified": null, "bytes": 3525}
Supplied lines: 1-60 (complete file)
```text
# EvE-WHMapper
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) ![GitHub top language](https://img.shields.io/github/languages/top/pfh59/eve-whmapper) ![GitHub language count](https://img.shields.io/github/languages/count/pfh59/eve-whmapper) [![Continous Integration and Deployment](https://github.com/pfh59/eve-whmapper/actions/workflows/ci-cd.yaml/badge.svg)](https://github.com/pfh59/eve-whmapper/actions/workflows/ci-cd.yaml) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=pfh59_eve-whmapper&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=pfh59_eve-whmapper) ![GitHub commit activity (main)](https://img.shields.io/github/commit-activity/m/pfh59/eve-whmapper) ![GitHub Release](https://img.shields.io/github/v/release/pfh59/eve-whmapper) ![Downloads (all assets, all releases)](https://img.shields.io/github/downloads/pfh59/eve-whmapper/total) ![GitHub Downloads (all assets, latest release)](https://img.shields.io/github/downloads/pfh59/eve-whmapper/latest/total)

EvE-WHMapper is a lightweight wormhole mapping and planning tool for EVE Online. It was originally inspired by [Pathfinder](https://github.com/exodus4d/pathfinder) and has been redesigned to be easier to deploy, maintain, and use in modern fleets and wormhole groups.

Key goals:
- Lightweight and fast
- Simple to deploy and administrate
- Easy to maintain over time

## Core Features

### Authentication
- CCP SSO login
- ESI API integration
- Multi-account support

### Access Control & Administration
- Define administration access lists per character
- Control Eve-WHMapper access for alliances, corporations, and characters
- Configure per-map access lists

### Map Module
- Share maps with other players and alts
- Track pilots and their current locations
- Automatic location tracking via ESI
- Auto-tag multi-system targets with the same class using A/B/C markers (or adjust manually with `+` / `-` or `Up` / `Down` keys)
- Add systems manually via right-click
- Select multiple systems with `Ctrl` + left click and move them together
- Link two systems by selecting them and pressing `L`
- Edit existing system connection links
- Lock systems to prevent accidental moves

### Route Planner Module
- Calculate optimal travel paths between systems—using both stargates and mapped wormholes
- Support route planning for individuals or fleets moving across your chain

### Jump Module
- Track and summarize all jumps between two systems
- Display hole size and current status (e.g., Normal / Critical)
- Show first and last jump information
- Keep a detailed log of each pilot and ship that passes through

## Hosting & Public Instance

EvE-WHMapper can be self-hosted using Docker, Kubernetes, or other deployment options described in the documentation.

For hosted usage, a public instance is available at [https://www.whmapper.ovh](https://www.whmapper.ovh), where you can create and manage your own Eve WHMapper space for an alliance, corporation, or personal use.

## Documentation

Full documentation (installation, configuration, modules, and usage guides) is available at: [https://pfh59.github.io/eve-whmapper-docs/home](https://pfh59.github.io/eve-whmapper-docs/home).

## Contributing

Contributions are welcome. Please see the repository's contributing guidelines in `CONTRIBUTING.md` before opening issues or pull requests.

## License

This project is released under the [MIT License](https://opensource.org/licenses/MIT).
```

## pfh59/eve-whmapper / src/WHMapper/WHMapper.csproj
Commit: 2a493fad9acec9a8e15b619f7943ae8b6e7f30da
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/WHMapper.csproj
Receipt: {"url": "https://raw.githubusercontent.com/pfh59/eve-whmapper/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/src/WHMapper/WHMapper.csproj", "retrieved_at": "2026-11-02T15:49:06.542909+00:00", "sha256": "c6980392aa7d3e53d218067640cdebfc26ea2c8f5808b4faad524a74b24177c3", "etag": "\"720e73317872503adb13cbd6b13b05f9807e2e18f66f6fb11f12aac8a1c6fe74\"", "last_modified": null, "bytes": 2927}
Supplied lines: 1-51 (complete file)
```text
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net10.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
    <UserSecretsId>4a1af26f-e1f0-4229-b68c-16e61e58037d</UserSecretsId>
    <Version>0.0.0</Version>
    <SatelliteResourceLanguages>en</SatelliteResourceLanguages>
  </PropertyGroup>

  <ItemGroup>
    <None Include="Services/BrowserClientIdProvider/IBrowserClientIdProvider.cs" />
  </ItemGroup>

  <ItemGroup>
    <EmbeddedResource Include="Resources/wh-effects.json" />
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.EntityFrameworkCore" Version="10.*" />
    <PackageReference Include="Microsoft.Extensions.Http.Resilience" Version="10.9.0" />
    <PackageReference Include="MudBlazor" Version="9.9.0" />
    <PackageReference Include="Serilog.AspNetCore" Version="10.*" />
    <PackageReference Include="Serilog.Settings.Configuration" Version="10.*" />
    <PackageReference Include="Serilog.Sinks.File" Version="7.0.0" />
    <PackageReference Include="Z.Blazor.Diagrams" Version="3.0.4.1" />
    <PackageReference Include="YamlDotNet" Version="18.*" />
    <PackageReference Include="FluentValidation" Version="12.*" />
    <PackageReference Include="Microsoft.IdentityModel.Protocols.OpenIdConnect" Version="8.22.0" />
    <PackageReference Include="Microsoft.AspNetCore.SignalR.Client" Version="10.*" />
    <PackageReference Include="FibonacciHeap" Version="2.0.2" />
    <PackageReference Include="Microsoft.AspNetCore.Authentication.JwtBearer" Version="10.*" />
    <PackageReference Include="Npgsql" Version="10.*" />
    <PackageReference Include="Npgsql.EntityFrameworkCore.PostgreSQL" Version="10.*" />
    <PackageReference Include="Microsoft.IdentityModel.JsonWebTokens" Version="8.22.0" />
    <PackageReference Include="Microsoft.AspNetCore.Authentication.OpenIdConnect" Version="10.*" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Design" Version="10.*" />
    <PackageReference Include="Microsoft.Extensions.Caching.StackExchangeRedis" Version="10.*" />
    <PackageReference Include="Microsoft.AspNetCore.DataProtection.StackExchangeRedis" Version="10.*" />
    <PackageReference Include="Z.Blazor.Diagrams.Algorithms" Version="3.0.4.1" />
    <PackageReference Include="OpenTelemetry" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Exporter.OpenTelemetryProtocol" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Extensions.Hosting" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Instrumentation.AspNetCore" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.18.0" />
    <PackageReference Include="OpenTelemetry.Instrumentation.Process" Version="1.18.0-rc.1" />
    <PackageReference Include="OpenTelemetry.Instrumentation.Runtime" Version="1.18.0" />
  </ItemGroup>

</Project>

```

## pfh59/eve-whmapper / deploy/docker/eve-whmapper/docker-compose.yml
Commit: 2a493fad9acec9a8e15b619f7943ae8b6e7f30da
Source: https://github.com/pfh59/eve-whmapper/blob/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/deploy/docker/eve-whmapper/docker-compose.yml
Receipt: {"url": "https://raw.githubusercontent.com/pfh59/eve-whmapper/2a493fad9acec9a8e15b619f7943ae8b6e7f30da/deploy/docker/eve-whmapper/docker-compose.yml", "retrieved_at": "2026-11-02T15:49:12.659086+00:00", "sha256": "9d3a676fcd80bde5421ebbe1abd49075443da9eb18736dce487a48dc51417187", "etag": "\"feee5def58c6645ea4f5f7fb9a4abebf79e2b8096bfc71d7333e6c242bfff413\"", "last_modified": null, "bytes": 1051}
Supplied lines: 1-46 (complete file)
```text
services:
  db:
    image: postgres:17-alpine
    restart: always
    environment:
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-secret}
      POSTGRES_DB: whmapper
      PGDATA: /data/postgres
    volumes:
     - postgres:/data/postgres
    networks:
     - net

  redis:
    image: redis:8-alpine
    restart: always
    networks:
     - net

  whmapper:
    image: ghcr.io/pfh59/eve-whmapper:latest
    restart: unless-stopped
    environment:
     - EveSSO__ClientId=xxxxxxxxx
     - EveSSO__Secret=xxxxxxxxx
     - ConnectionStrings__DatabaseConnection=server=db;port=5432;database=whmapper;User Id=postgres;Password=secret
     - ConnectionStrings__RedisConnection=redis:6379
     - Serilog__MinimumLevel__Default=Warning
     - Serilog__MinimumLevel__Override__Microsoft.EntityFrameworkCore.Database.Command=Warning
    links:
      - db
      - redis
    depends_on:
      - db
      - redis
    networks:
     - net
    volumes:
     - ./Logs:/app/Logs

networks:
  net:

volumes:
    postgres:
```

## Evidence limits
Public commit pins and HTTP snapshot hashes establish what was fetched, not that an implementation is secure or works. Root MIT notices do not settle transitive licences, assets, game-data rights or the separate CCP developer agreement. The official agreement is at https://developers.eveonline.com/license-agreement and requires an owner review; no agreement was accepted and no commercial/ISK model is approved by this packet.
