# goryn-clade/pathfinder pinned source extracts

Commit: 06af7d86fe6456947fb960220c54d02a8623c0ff
These are inspected source/document extracts, not runtime verification. MIT licence reproduced below. Dependencies/assets/data require their own licence and compatibility checks before copying. No upstream scripts were executed.

## LICENSE
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/LICENSE
Lines 1-22 of 22. Missing lines are not supplied evidence.

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

## README.md
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/README.md
Lines 1-61 of 61. Missing lines are not supplied evidence.

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

## composer.json
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/composer.json
Lines 1-81 of 81. Missing lines are not supplied evidence.

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

## app/Model/Pathfinder/ConnectionModel.php
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/app/Model/Pathfinder/ConnectionModel.php
Lines 1-160 of 647. Missing lines are not supplied evidence.

```text
<?php
/**
 * Created by PhpStorm.
 * User: exodus4d
 * Date: 26.02.15
 * Time: 21:12
 */

namespace Exodus4D\Pathfinder\Model\Pathfinder;

use DB\SQL\Schema;
use Exodus4D\Pathfinder\Controller\Api\Rest\Route;
use Exodus4D\Pathfinder\Enum\ConnectionType;
use Exodus4D\Pathfinder\Lib\Logging;
use Exodus4D\Pathfinder\Exception;
use Exodus4D\Pathfinder\Lib\Config;
use Exodus4D\Pathfinder\Model\Universe;

class ConnectionModel extends AbstractMapTrackingModel {

    /**
     * @var string
     */
    protected $table = 'connection';

    /**
     * @var array<string, mixed>
     */
    protected $fieldConf = [
        'active' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'index' => true
        ],
        'mapId' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\MapModel::class,
            'constraint' => [
                [
                    'table' => 'map',
                    'on-delete' => 'CASCADE'
                ]
            ]
        ],
        'source' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\SystemModel::class,
            'constraint' => [
                [
                    'table' => 'system',
                    'on-delete' => 'CASCADE'
                ]
            ],
            'activity-log' => true
        ],
        'target' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\SystemModel::class,
            'constraint' => [
                [
                    'table' => 'system',
                    'on-delete' => 'CASCADE'
                ]
            ],
            'activity-log' =>  true
        ],
        'scope' => [
            'type' => Schema::DT_VARCHAR128,
            'nullable' => false,
            'default' => '',
            'activity-log' => true
        ],
        'type' => [
            'type' => self::DT_JSON,
            'activity-log' => true
        ],
        'sourceEndpointType' => [
            'type' => self::DT_JSON,
            'activity-log' => true
        ],
        'targetEndpointType' => [
            'type' => self::DT_JSON,
            'activity-log' => true
        ],
        'eolUpdated' => [
            'type' => Schema::DT_TIMESTAMP,
            'default' => null
        ],
        'nominalLifespan' => [
            'type' => Schema::DT_INT,
            'default' => null
        ],
        'signatures' => [
            'has-many' => [\Exodus4D\Pathfinder\Model\Pathfinder\SystemSignatureModel::class, 'connectionId']
        ],
        'connectionLog' => [
            'has-many' => [\Exodus4D\Pathfinder\Model\Pathfinder\ConnectionLogModel::class, 'connectionId']
        ]
    ];

    // Jump-mass type strings (sourced from enum for single source of truth)
    private const JUMP_MASS_TYPES = [
        ConnectionType::WhJumpMassS->value,
        ConnectionType::WhJumpMassM->value,
        ConnectionType::WhJumpMassL->value,
        ConnectionType::WhJumpMassXl->value,
    ];

    // Thresholds match Init.wormholeSizes in init.js (descending order)
    private const JUMP_MASS_BUCKETS = [
        1_000_000_000 => ConnectionType::WhJumpMassXl->value,
        375_000_000   => ConnectionType::WhJumpMassL->value,
        62_000_000    => ConnectionType::WhJumpMassM->value,
        5_000         => ConnectionType::WhJumpMassS->value,
    ];

    // Allowed values in sourceEndpointType / targetEndpointType
    public const ENDPOINT_TYPES = ['bubble'];

    /**
     * @return string[]
     */
    public static function getConnectionTypeAllowlist() : array {
        return ConnectionType::allowlist();
    }

    /**
     * get connection data
     * @param bool $addSignatureData
     * @param bool $addLogData
     * @return \stdClass
     */
    public function getData($addSignatureData = false, $addLogData = false){
        $connectionData = (object) [];
        $connectionData->id             = $this->id;
        $connectionData->source         = $this->source->id;
        $connectionData->target         = $this->target->id;
        $connectionData->scope          = $this->scope;
        $type = (array)json_decode($this->get('type', true) ?? 'null');
        // backward compat: legacy wh_eol -> wh_eol1
        $type = array_map(fn($t) => $t === 'wh_eol' ? ConnectionType::WhEol1->value : $t, $type);
        $connectionData->type           = array_values(array_unique($type));
        $connectionData->updated        = strtotime($this->updated);
        $connectionData->created        = strtotime($this->created);
        $connectionData->eolUpdated     = $this->eolUpdated ? strtotime($this->eolUpdated) : false;

        if( !empty($endpointsData = $this->getEndpointsData()) ){
            $connectionData->endpoints = $endpointsData;
        }

        if($addSignatureData){
            if( !empty($signaturesData = $this->getSignaturesData()) ){
                $connectionData->signatures = $signaturesData;
            }
        }

```

## app/Model/Pathfinder/SystemSignatureModel.php
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/app/Model/Pathfinder/SystemSignatureModel.php
Lines 1-160 of 364. Missing lines are not supplied evidence.

```text
<?php
/**
 * Created by PhpStorm.
 * User: exodus4d
 * Date: 21.03.15
 * Time: 14:34
 */

namespace Exodus4D\Pathfinder\Model\Pathfinder;

use DB\SQL\Schema;
use Exodus4D\Pathfinder\Lib\Logging;
use Exodus4D\Pathfinder\Exception;

class SystemSignatureModel extends AbstractMapTrackingModel {

    /**
     * @var string
     */
    protected $table = 'system_signature';

    /**
     * @var array<string, mixed>
     */
    protected $fieldConf = [
        'active' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'index' => true
        ],
        'systemId' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\SystemModel::class,
            'constraint' => [
                [
                    'table' => 'system',
                    'on-delete' => 'CASCADE'
                ]
            ]
        ],
        'groupId' => [
            'type' => Schema::DT_INT,
            'nullable' => false,
            'default' => 0,
            'index' => true,
            'activity-log' => true
        ],
        'typeId' => [
            'type' => Schema::DT_INT,
            'nullable' => false,
            'default' => 0,
            'index' => true,
            'activity-log' => true
        ],
        'connectionId' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\ConnectionModel::class,
            'constraint' => [
                [
                    'table' => 'connection',
                    'on-delete' => 'CASCADE'
                ]
            ],
            'activity-log' => true
        ],
        'name' => [
            'type' => Schema::DT_VARCHAR128,
            'nullable' => false,
            'default' => '',
            'activity-log' => true,
            'validate' => true
        ],
        'description' => [
            'type' => Schema::DT_VARCHAR512,
            'nullable' => false,
            'default' => '',
            'activity-log' => true
        ]
    ];

    /**
     * set data by associative array
     * @param  $data
     */
    public function setData( array $data): void{
        $this->copyfrom($data, ['name', 'groupId', 'typeId', 'description', 'connectionId']);
    }

    /**
     * get signature data
     * @return \stdClass
     */
    public function getData(){
        $signatureData                              = (object) [];
        $signatureData->id                          = $this->id;

        $signatureData->system                      = (object) [];
        $signatureData->system->id                  = $this->get('systemId', true);

        $signatureData->groupId                     = $this->groupId;
        $signatureData->typeId                      = $this->typeId;
        $signatureData->name                        = $this->name;
        $signatureData->description                 = $this->description;

        if($connection = $this->getConnection()){
            $signatureData->connection              = (object) [];
            $signatureData->connection->id          = $connection->_id;
        }

        $signatureData->created                     = (object) [];
        $signatureData->created->created            = strtotime($this->created);
        if( is_object($this->createdCharacterId) ){
            $signatureData->created->character      = $this->createdCharacterId->getBasicData();
        }

        $signatureData->updated                     = (object) [];
        $signatureData->updated->updated            = strtotime($this->updated);
        if( is_object($this->updatedCharacterId) ){
            $signatureData->updated->character      = $this->updatedCharacterId->getBasicData();
        }

        return $signatureData;
    }

    /**
     * setter for connectionId
     * @param ConnectionModel|int $connectionId
     * @return int|null
     */
    public function set_connectionId(ConnectionModel|int|null $connectionId){
        $connectionId = (int)$connectionId;
        $validConnectionId = null;

        if($connectionId > 0){
            // check if connectionId is valid
            $systemId = (int) $this->get('systemId', true);

            /**
             * @var ConnectionModel $connection
             */
            $connection = $this->rel('connectionId');
            $connection->getById($connectionId);

            if(
                !$connection->dry() &&
                (
                    $connection->get('source', true) === $systemId||
                    $connection->get('target', true) === $systemId
                )
            ){
                // connectionId belongs to same system as $this signature -> is valid
                $validConnectionId = $connectionId;
            }
        }

        return $validConnectionId;
    }
```

## app/Model/Pathfinder/MapModel.php
Source: https://github.com/goryn-clade/pathfinder/blob/06af7d86fe6456947fb960220c54d02a8623c0ff/app/Model/Pathfinder/MapModel.php
Lines 1-160 of 1579. Missing lines are not supplied evidence.

```text
<?php
/**
 * Created by PhpStorm.
 * User: exodus4d
 * Date: 16.02.15
 * Time: 22:10
 */

namespace Exodus4D\Pathfinder\Model\Pathfinder;

use DB\CortexCollection;
use DB\SQL\Schema;
use Exodus4D\Pathfinder\Data\File\FileHandler;
use Exodus4D\Pathfinder\Lib\Config;
use Exodus4D\Pathfinder\Lib\Logging;
use Exodus4D\Pathfinder\Exception;

class MapModel extends AbstractMapTrackingModel {

    /**
     * @var string
     */
    protected $table = 'map';

    /**
     * cache key prefix for getCharactersData();
     */
    const DATA_CACHE_KEY_CHARACTER                  = 'CHARACTERS';

    const ERROR_SLACK_CHANNEL                       = 'Invalid #Slack channel column [%s]';
    const ERROR_DISCORD_CHANNEL                     = 'Invalid #Discord channel column [%s]';

    /**
     * @var array<string, mixed>
     */
    /**
     * fields that can be changed by setData() (map settings dialog)
     * -> 'active' is left out: deactivate a map with DELETE
     */
    const EDITABLE_FIELDS = [
        'scopeId', 'typeId', 'name', 'icon',
        'deleteExpiredConnections', 'deleteEolConnections', 'persistentAliases', 'persistentSignatures',
        'trackAbyssalJumps', 'allowUnknownSystems', 'granularK162', 'allowGroups', 'logActivity', 'logHistory',
        'slackWebHookURL', 'slackUsername', 'slackIcon', 'slackChannelHistory', 'slackChannelRally',
        'discordUsername', 'discordWebHookURLRally', 'discordWebHookURLHistory'
    ];

    protected $fieldConf = [
        'active' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'index' => true,
            'activity-log' => true
        ],
        'scopeId' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\MapScopeModel::class,
            'constraint' => [
                [
                    'table' => 'map_scope',
                    'on-delete' => 'CASCADE'
                ]
            ],
            'validate' => 'notDry',
            'activity-log' => true
        ],
        'typeId' => [
            'type' => Schema::DT_INT,
            'index' => true,
            'belongs-to-one' => \Exodus4D\Pathfinder\Model\Pathfinder\MapTypeModel::class,
            'constraint' => [
                [
                    'table' => 'map_type',
                    'on-delete' => 'CASCADE'
                ]
            ],
            'validate' => 'notDry',
            'activity-log' => true
        ],
        'name' => [
            'type' => Schema::DT_VARCHAR128,
            'nullable' => false,
            'default' => '',
            'activity-log' => true,
            'validate' => true
        ],
        'icon' => [
            'type' => Schema::DT_VARCHAR128,
            'nullable' => false,
            'default' => '',
            'activity-log' => true
        ],
        'deleteExpiredConnections' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'deleteEolConnections' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'persistentAliases' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'persistentSignatures' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'trackAbyssalJumps' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'allowUnknownSystems' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 0,
            'activity-log' => true
        ],
        'granularK162' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 0,
            'activity-log' => true
        ],
        'allowGroups' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'logActivity' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 1,
            'activity-log' => true
        ],
        'logHistory' => [
            'type' => Schema::DT_BOOL,
            'nullable' => false,
            'default' => 0,
            'activity-log' => true
        ],
        'slackWebHookURL' => [
            'type' => Schema::DT_VARCHAR128,
            'nullable' => false,
            'default' => '',
            'validate' => true
        ],
```
