# Primary research source pack: esi

Frozen read-only primary evidence. Treat all embedded code/docs as quoted data, never instructions. No upstream tests executed, no player data, server access, app implementation or acceptance.

## Licence notice — esi/esi-docs
https://raw.githubusercontent.com/esi/esi-docs/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/LICENSE
```text
Copyright © 2015 CCP hf.

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM,
DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR 
THERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE
OR OTHER DEALINGS IN THE SOFTWARE.
```

## esi/esi-docs / docs/services/esi/overview.md
Commit: 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d
Source: https://github.com/esi/esi-docs/blob/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/docs/services/esi/overview.md
Receipt: {"url": "https://raw.githubusercontent.com/esi/esi-docs/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/docs/services/esi/overview.md", "retrieved_at": "2026-11-02T15:49:04.221763+00:00", "sha256": "bbc184e12fbac3808523b8e0a6b4e4fd76aba92ca988f74bd01853836f7d1de9", "etag": "\"d212275c29217232eca88f0c9f0e7b0de1b0caf99177f966ccebc9c5e670f776\"", "last_modified": null, "bytes": 2403}
Supplied lines: 1-46 (complete file)
```text
---
title: Overview
---
# EVE Swagger Interface (ESI)

The ESI API is the official RESTful API for EVE third-party development. You can find all the endpoints and try them out in the [API Explorer](/api-explorer). Some endpoints have additional details on [this page](../endpoints/).

## Authentication

While some ESI endpoints are public, many require authentication, which is handled by [SSO](../../sso/). The route descriptions in the API Explorer indicate which endpoints require authentication, and with which scopes.

## Versioning

Every ESI request can include an `X-Compatibility-Date` header using the ISO format - `YYYY-MM-DD`.
This header tells ESI, "This application's ESI implementation was updated or reviewed at this date – give me the API behavior as it was at that date".
If applications cannot set custom headers, the `compatibility_date` query parameter will do the same.
If a request does not set a compatibility date, the oldest available compatibility date is used.

The date cannot be in the future, neither can it below a minimum threshold (the "oldest" versions available).
If this minimum bar is raised, this will be clearly communicated via dev-blogs.

The API changes date at 11:00 UTC.
So if you want to use the date of today, use (pseudocode): `now() - 11 * 60 * 60`, to get the current date of the API.

### New Compatibility Date

The following changes will always be released under a new compatibility date:

- Adding of new routes.
- Adding or changing of (now to be) required request parameters.
- Changing the type of request parameters / response fields / response headers.
- Removing of request parameters.
- Removing of response fields / response headers / enum values.

The following changes will always be released as part of the existing compatibility dates:

- Adding of optional request parameters.
- Adding of response fields / response headers / enum values.

## Support

ESI has its own issues repository at [esi-issues](https://github.com/esi/esi-issues). From there you can raise issues or ask for new features. Also see the general [support page](../../../support/).

## ESI Bans

If you have been banned from ESI, responses to your requests will point you to the EVE Online support system. Please follow the instructions. Circumventing the ban can result in further action being taken, up to and including a permanent ban for all of your accounts.

```

## esi/esi-docs / docs/services/esi/rate-limiting.md
Commit: 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d
Source: https://github.com/esi/esi-docs/blob/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/docs/services/esi/rate-limiting.md
Receipt: {"url": "https://raw.githubusercontent.com/esi/esi-docs/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/docs/services/esi/rate-limiting.md", "retrieved_at": "2026-11-02T15:49:04.570577+00:00", "sha256": "05bcba0b7beb70d85555519613f049935fc5a5fb0accd61e7ae640e2e008e5ff", "etag": "\"aac04f2ee870dfc2d46a0aa794b3adc8610b39c597d17894b028cad49489c886\"", "last_modified": null, "bytes": 5010}
Supplied lines: 1-101 (complete file)
```text
---
title: Rate Limiting
---
# Rate Limiting

ESI implements [floating window rate limiting](https://smudge.ai/blog/ratelimit-algorithms#sliding-windows) to ensure fair usage across all applications.
The intention of the rate limit is to show third party developers where the line is; but please don't take it for a challenge to constantly find the line.
In most cases you should be fine with far less requests than the rate limit allows you.

!!! important

    Rate limiting isn't active on all routes yet.
    Check the OpenAPI Specs or the HTTP response headers for up-to-date information.

!!! warning

    For routes that do not have this new rate limiting enabled, there is still an older "error rate limit" active.
    This allows at most 100 non-2xx/3xx responses per minute. After that, it will return 420s on all ESI routes, even those with the new rate limiting enabled.
    The headers described in this document are mutually exclusive to those described in the Error Limit documentation found under "Best Practices".

!!! important

    Some routes also have a rate limiter deep in EVE Server code.
    This can also cause 429s to be returned, without the rate limiter headers indicating why.
    We are working on deprecating these, but in the mean time, be aware this can be the case.

## Floating Window

A floating window is a mathematical approximation where tokens consumed by a request are released back to your bucket after the window size has passed.

For example, with a 15-minute window:

- If you make a request at 10:00 AM that costs 2 tokens, those 2 tokens will be returned to your bucket around 10:15 AM.
- If you make another request at 10:05 AM that costs 1 token, that token will be returned around 10:20 AM.

This creates a sliding window where your token consumption is tracked continuously, and tokens are freed up as time passes from when they were originally consumed.

## Bucket System

Each `rate limit group` and `userID` pair is assigned their own bucket.

- `rate limit group`: Each route is assigned to a rate limit group. This is mentioned both in the response headers as in the API specifications.
- `userID`:
    - Authenticated routes: `<applicationID>:<characterID>` from the Access Token.
    - Non-authenticated routes: `<sourceIP>` (or `<sourceIP>:<applicationID>` if an Access Token is supplied).

On each request, ESI verifies that you haven't exceeded the maximum tokens allocated for your assigned bucket.
If you have exceeded that limit, you receive a 429, together with a `Retry-After` header.
This header indicates, in seconds, when you will have enough tokens to make a request that won't be rate limited.

!!! note

    The reason the `userID` is a combination of both the `applicationID` and `characterID`, is to ensure popular apps have to obey by the same limits as newly created apps.
    Some token limits might look small, but remember: they are per applicationID/characterID pair.

## Token System

Every request consumes tokens based on the response status:

| Status Code | Token Cost | Reasoning                                                        |
|-------------|------------|------------------------------------------------------------------|
| 2XX         | 2 tokens   |                                                                  |
| 3XX         | 1 token    | Promote the use of `If-Modified-Since` and `If-Match`.           |
| 4XX         | 5 tokens   | Discourage hitting user-errors. Does not apply to 429 responses. |
| 5XX         | 0 tokens   | You shouldn't be penalized for server-side errors.               |

## Rate Limit Headers

The following headers are included in HTTP response for routes under rate limiting:

- `X-Ratelimit-Group`: Route group identifier.
- `X-Ratelimit-Limit`: Total tokens per window (format: `150/15m`).
    - `m`: minutes.
    - `h`: hours.
- `X-Ratelimit-Remaining`: Available tokens remaining.
- `X-Ratelimit-Used`: Tokens consumed by this request.

And if you are rate-limited (429):

- `Retry-After`: indicates, in seconds, when to try again.

## OpenAPI Specs extension

For each route that has rate limiting active, the OpenAPI specs announces this via the `x-rate-limit` extension.
This contains three fields:

- `group`: the rate limit group this route belongs to.
- `window-size`: the size of the window.
- `max-tokens`: the maximum amount of tokens allowed per `window-size`.

Each route in the same group will show the same `window-size` and `max-tokens`.

## Best Practices

- Don't operate at the limit.
- If the `X-Ratelimit-Remaining` is approaching zero, start to slow down.
- Spread requests over time rather than bursting constantly.
- If you need to burst, that is fine; just not every window-size.
- Use staggered scheduling for periodic requests when possible. Ideally not `*/5` cronjobs. But rather: 5 minutes after the last job was finished.
- Respect cache times to minimize unnecessary requests.
- For Error Limiting, see [Best Practices](./best-practices.md)

```

## esi/esi-docs / docs/services/esi/best-practices.md
Commit: 98b42d5ac69fb9c57fbc688053d6ae48183dbd0d
Source: https://github.com/esi/esi-docs/blob/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/docs/services/esi/best-practices.md
Receipt: {"url": "https://raw.githubusercontent.com/esi/esi-docs/98b42d5ac69fb9c57fbc688053d6ae48183dbd0d/docs/services/esi/best-practices.md", "retrieved_at": "2026-11-02T15:49:04.915083+00:00", "sha256": "f56bbb52daa9ba23c32074216df285e73678663821ffd6e9a5bb371839de653c", "etag": "\"6a65d358561bd71e90d4adf0528bd4e7fcd45b64b19f500ff14e59452b41cf43\"", "last_modified": null, "bytes": 6181}
Supplied lines: 1-105 (complete file)
```text
---
title: Best Practices for ESI
---
# Best Practices for ESI

The following are some best practices when you interact with ESI. Not all are hard requirements, but they are highly recommended to ensure a smooth experience for both you and CCP. Remember that the ESI API is a shared resource, do not abuse it.

## User Agents

All ESI requests **should** contain User Agent information indicating the application making the request. This information can be used by CCP to identify the source of requests, and in some cases, to contact the developers if there are issues with the application.

It should be noted that for browser applications, you may not be able to set the `User-Agent` header directly [1]. In this case, you should use the `X-User-Agent` header instead. If neither of these options is available, you can use the `user_agent` query parameter [2].

A simple flowchart to help you decide how to send your user agent information:

{% raw %}
``` mermaid
flowchart LR
    Q1{{Can you set HTTP headers?}}
    Q2{{Is your app a browser application?}}
    A1[Use 'User-Agent' Header]
    A2["Use 'X-User-Agent' Header [1]"]
    A3["Use 'user_agent' Query Parameter [2]"]
    Q1 -->|Yes| Q2
    Q1 -->|No| A3
    Q2 -->|Yes| A2
    Q2 -->|No| A1
```
{% endraw %}

!!! note "[1] `User-Agent` vs `X-User-Agent` Header"

    The `User-Agent` header used to be [forbidden](https://developer.mozilla.org/en-US/docs/Glossary/Forbidden_request_header), but no longer is. However, Chrome and Chromium-based browsers still silently drop the header from Fetch requests. This is why we recommend using `X-User-Agent` for browser applications instead.

!!! note "[2] `user_agent` Query Parameter"

    If you are unable to set request headers, you can use the `user_agent` query parameter to still send your user agent information. Keep in mind that like any other query parameter, this will need to be URL-encoded.

### Information to transmit

The User Agent information you send should contain one or more of the following :

- An Email Address (**Strongly Preferred**) `(foo@example.com)`
- App Name with version (**Strongly Preferred**) `AppName/1.2.3`
- A URL to Source Code `(+https://github.com/your/repository)`
- A Discord Username `(discord:username)`
- An EVE Character `(eve:charactername)`

While User Agents are not a defined web standard, the MDN provides a thoroughly documented set of examples <https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent>; following these standards will ensure your useragent is well understood.

### Libraries/frameworks

If your application consists of multiple _products_ such as an upstream library, or if you are a plugin/extension of a larger app, you may like to list these in _narrow to broad_ order, with your useragent being more to less precise. You should _always_ include the source of the code generating the request.

```text
PluginName/1.2.3 (foo@example.com; +https://github.com/) AppName/1.2.3 LibraryName/1.2.3
```

### Examples

```
AllianceAuth/1.2.3 (foo@example.com; +https://gitlab.com/allianceauth/allianceauth) DjangoESI/1.2.3
AASRP/1.2.3 (foo@example.comm; +https://github.com/ppfeufer/aa-srp) DjangoESI/1.2.3
eveseat:eveapi/5.0.22 (admin contact: foo@example) (https://github.com/eveseat/seat) eveseat:seat/5.0.x-dev eveseat:web/5.0.23 eveseat:eveapi/5.0.22
RIFT/1.2.3 (foo@example.com)
```

## Requests Limit

ESI can limit your requests in two way : with global errors limits, and with endpoint-specific bucket limit.

Not abiding to the information transmitted can lead to your app being **banned**, for various time, from accessing the resources.

### Error limit

ESI limits how many errors you’re allowed to get within a set time frame. This Limit uses a fixed time frame, in contrast to the Bucket Limit which is a sliding window. Once you reach the error limit, all your request are automatically discarded until the end of the time frame.

Error limit headers:  
`X-ESI-Error-Limit-Remain` errors left in this time frame.  
`X-ESI-Error-Limit-Reset` seconds left until next time frame and errors reset to zero.

These headers are mutually exclusive to those described in the Bucket based Rate Limit.

The details are explained in this blog post: [Error Rate Limiting](/blog/error-rate-limiting-imminent)

### Bucket Limit

This limitation is described in [its own dedicated page](./rate-limiting.md)

## Caching

The ESI acts as both an http handler for resources available in the monolith, and a cache manager of those resources' representation. You can get a benefit from the caching in several ways, depending on the request you send.

The `expires` header represents when the resource cache in ESI should expire, that is when updated data should be available.
You should not update before that. If you update before, the best case scenario is that you will get a cached result, wasting resources on both side of the request. In the worst case scenario you will get new data, and it may count as circumventing the ESI caching. Circumventing the ESI caching can get you banned from ESI.

The `last-modified` header indicates when the data was last updated in the cache.

The `ETag` header is a hash of the content. Once you have received that header with a response, in a subsequent request you can add the `If-None-Match` header set to the last retrieved value. If the data did not change since the last cached value, the server will return a `304` response code instead of e.g. `200`, meaning there is no change to handle.

Notes:

- When requesting a paginated resource, the `last-modified` header should be the same for all the pages of a single resource. Checking this constraint allows you to validate the data retrieved, typically by avoiding the case where the data is refreshed between the calls to two different pages. This issue can also happen outside of ESI cache refresh.
- Some resources may not provide such headers, typically POST methods have no cache information, even when they still actually have an internal cache.
- Static data should have the same shared caching information. That is, planets, moons, types, etc. paths should return the same caching headers.

```

## Public discovery and selected ESI schema metadata
```json
{
  "compatibility_date_requested": "2026-08-18",
  "spec_info": {
    "contact": {
      "name": "ESI Support",
      "url": "https://developers.eveonline.com/docs/support/"
    },
    "license": {
      "name": "EVE Developer License",
      "url": "https://developers.eveonline.com/license-agreement"
    },
    "termsOfService": "https://support.eveonline.com/hc/en-us/articles/8414770561948-EVE-Online-Terms-of-Service",
    "title": "EVE SKINR Ingenuity (ESI) - tranquility",
    "version": "2026-08-18"
  },
  "selected_paths": {
    "/characters/{character_id}/corporationhistory": {
      "get": {
        "description": "Get a list of all the corporations a character has been a member of",
        "operationId": "GetCharactersCharacterIdCorporationhistory",
        "parameters": [
          {
            "description": "The ID of the character",
            "in": "path",
            "name": "character_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/CharacterID"
            }
          },
          {
            "$ref": "#/components/parameters/AcceptLanguage"
          },
          {
            "$ref": "#/components/parameters/IfNoneMatch"
          },
          {
            "$ref": "#/components/parameters/CompatibilityDate"
          },
          {
            "$ref": "#/components/parameters/Tenant"
          },
          {
            "$ref": "#/components/parameters/IfModifiedSince"
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CharactersCharacterIdCorporationhistoryGet"
                }
              }
            },
            "description": "OK",
            "headers": {
              "Cache-Control": {
                "$ref": "#/components/headers/CacheControl"
              },
              "ETag": {
                "$ref": "#/components/headers/ETag"
              },
              "Last-Modified": {
                "$ref": "#/components/headers/LastModified"
              }
            }
          },
          "default": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            },
            "description": "Error"
          }
        },
        "summary": "Get corporation history",
        "tags": [
          "Character"
        ],
        "x-cache-age": 86400,
        "x-client-cache-ttl": 86400,
        "x-compatibility-date": "2020-01-01",
        "x-server-cache-mode": "ttl-based",
        "x-server-cache-ttl": 86400
      }
    },
    "/characters/{character_id}/location": {
      "get": {
        "description": "Get the current location of a character, including the station or structure it is docked in.",
        "operationId": "GetCharactersCharacterIdLocation",
        "parameters": [
          {
            "description": "The ID of the character",
            "in": "path",
            "name": "character_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/CharacterID",
              "description": "The ID of the character"
            }
          },
          {
            "$ref": "#/components/parameters/AcceptLanguage"
          },
          {
            "$ref": "#/components/parameters/IfNoneMatch"
          },
          {
            "$ref": "#/components/parameters/CompatibilityDate"
          },
          {
            "$ref": "#/components/parameters/Tenant"
          },
          {
            "$ref": "#/components/parameters/IfModifiedSince"
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CharactersLocation"
                }
              }
            },
            "description": "OK",
            "headers": {
              "Cache-Control": {
                "$ref": "#/components/headers/CacheControl"
              },
              "ETag": {
                "$ref": "#/components/headers/ETag"
              },
              "Last-Modified": {
                "$ref": "#/components/headers/LastModified"
              }
            }
          },
          "default": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            },
            "description": "Error"
          }
        },
        "security": [
          {
            "OAuth2": [
              "esi-location.read_location.v1"
            ]
          }
        ],
        "summary": "Get character location",
        "tags": [
          "Location"
        ],
        "x-cache-age": 5,
        "x-cache-mode": "event-based",
        "x-client-cache-ttl": 5,
        "x-compatibility-date": "2020-01-01",
        "x-rate-limit": {
          "group": "char-location",
          "max-tokens": 1200,
          "window-size": "15m"
        },
        "x-server-cache-mode": "event-based"
      }
    },
    "/characters/{character_id}/online": {
      "get": {
        "description": "Get whether a character is online, and its login statistics.",
        "operationId": "GetCharactersCharacterIdOnline",
        "parameters": [
          {
            "description": "The ID of the character",
            "in": "path",
            "name": "character_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/CharacterID",
              "description": "The ID of the character"
            }
          },
          {
            "$ref": "#/components/parameters/AcceptLanguage"
          },
          {
            "$ref": "#/components/parameters/IfNoneMatch"
          },
          {
            "$ref": "#/components/parameters/CompatibilityDate"
          },
          {
            "$ref": "#/components/parameters/Tenant"
          },
          {
            "$ref": "#/components/parameters/IfModifiedSince"
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CharactersOnline"
                }
              }
            },
            "description": "OK",
            "headers": {
              "Cache-Control": {
                "$ref": "#/components/headers/CacheControl"
              },
              "ETag": {
                "$ref": "#/components/headers/ETag"
              },
              "Last-Modified": {
                "$ref": "#/components/headers/LastModified"
              }
            }
          },
          "default": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            },
            "description": "Error"
          }
        },
        "security": [
          {
            "OAuth2": [
              "esi-location.read_online.v1"
            ]
          }
        ],
        "summary": "Get character online",
        "tags": [
          "Location"
        ],
        "x-cache-age": 60,
        "x-cache-mode": "event-based",
        "x-client-cache-ttl": 60,
        "x-compatibility-date": "2020-01-01",
        "x-rate-limit": {
          "group": "char-location",
          "max-tokens": 1200,
          "window-size": "15m"
        },
        "x-server-cache-mode": "event-based"
      }
    },
    "/characters/{character_id}/ship": {
      "get": {
        "description": "Get the ship a character is currently in.",
        "operationId": "GetCharactersCharacterIdShip",
        "parameters": [
          {
            "description": "The ID of the character",
            "in": "path",
            "name": "character_id",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/CharacterID",
              "description": "The ID of the character"
            }
          },
          {
            "$ref": "#/components/parameters/AcceptLanguage"
          },
          {
            "$ref": "#/components/parameters/IfNoneMatch"
          },
          {
            "$ref": "#/components/parameters/CompatibilityDate"
          },
          {
            "$ref": "#/components/parameters/Tenant"
          },
          {
            "$ref": "#/components/parameters/IfModifiedSince"
          }
        ],
        "responses": {
          "200": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/CharactersShip"
                }
              }
            },
            "description": "OK",
            "headers": {
              "Cache-Control": {
                "$ref": "#/components/headers/CacheControl"
              },
              "ETag": {
                "$ref": "#/components/headers/ETag"
              },
              "Last-Modified": {
                "$ref": "#/components/headers/LastModified"
              }
            }
          },
          "default": {
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            },
            "description": "Error"
          }
        },
        "security": [
          {
            "OAuth2": [
              "esi-location.read_ship_type.v1"
            ]
          }
        ],
        "summary": "Get current ship",
        "tags": [
          "Location"
        ],
        "x-cache-age": 5,
        "x-cache-mode": "ttl-based",
        "x-client-cache-ttl": 5,
        "x-compatibility-date": "2020-01-01",
        "x-rate-limit": {
          "group": "char-location",
          "max-tokens": 1200,
          "window-size": "15m"
        },
        "x-server-cache-mode": "ttl-based",
        "x-server-cache-ttl": 5
      }
    }
  },
  "referenced_schemas": {
    "CharactersCharacterIdCorporationhistoryGet": {
      "items": {
        "properties": {
          "corporation_id": {
            "format": "int64",
            "type": "integer"
          },
          "is_deleted": {
            "description": "True if the corporation has been deleted",
            "type": "boolean"
          },
          "record_id": {
            "description": "An incrementing ID that can be used to canonically establish order of records in cases where dates may be ambiguous",
            "format": "int64",
            "type": "integer"
          },
          "start_date": {
            "format": "date-time",
            "type": "string"
          }
        },
        "required": [
          "start_date",
          "corporation_id",
          "record_id"
        ],
        "type": "object"
      },
      "type": "array"
    },
    "CharactersOnline": {
      "properties": {
        "last_login": {
          "description": "When the character last logged in",
          "examples": [
            "2017-01-02T03:04:05Z"
          ],
          "format": "date-time",
          "type": "string"
        },
        "last_logout": {
          "description": "When the character last logged out",
          "examples": [
            "2017-01-02T04:05:06Z"
          ],
          "format": "date-time",
          "type": "string"
        },
        "logins": {
          "description": "Total logins (all-time)",
          "examples": [
            9001
          ],
          "format": "int64",
          "type": "integer"
        },
        "online": {
          "description": "Whether the character is online",
          "type": "boolean"
        }
      },
      "required": [
        "online"
      ],
      "type": "object"
    },
    "CharacterID": {
      "examples": [
        90000001
      ],
      "format": "int64",
      "type": "integer",
      "x-common-model": "true"
    },
    "CharactersShip": {
      "properties": {
        "ship_item_id": {
          "$ref": "#/components/schemas/ItemID",
          "description": "Unique identifier for this ship"
        },
        "ship_name": {
          "description": "Name of this ship",
          "type": "string"
        },
        "ship_type_id": {
          "$ref": "#/components/schemas/TypeID",
          "description": "Type of the ship currently piloted"
        }
      },
      "required": [
        "ship_type_id",
        "ship_item_id",
        "ship_name"
      ],
      "type": "object"
    },
    "CharactersLocation": {
      "properties": {
        "solar_system_id": {
          "$ref": "#/components/schemas/SolarSystemID",
          "description": "Solar system the character is in"
        },
        "station_id": {
          "$ref": "#/components/schemas/StationID",
          "description": "Station the character is docked in"
        },
        "structure_id": {
          "$ref": "#/components/schemas/ItemID",
          "description": "Structure the character is docked in"
        }
      },
      "required": [
        "solar_system_id"
      ],
      "type": "object"
    },
    "Error": {
      "properties": {
        "details": {
          "description": "List of individual issues.",
          "items": {
            "$ref": "#/components/schemas/ErrorDetail"
          },
          "type": "array"
        },
        "error": {
          "description": "Error message.",
          "type": "string"
        },
        "status": {
          "description": "HTTP status code.",
          "format": "int64",
          "type": "integer"
        }
      },
      "required": [
        "error"
      ],
      "type": "object"
    },
    "TypeID": {
      "examples": [
        587
      ],
      "format": "int64",
      "type": "integer",
      "x-common-model": "true"
    },
    "SolarSystemID": {
      "examples": [
        30000001
      ],
      "format": "int64",
      "type": "integer",
      "x-common-model": "true"
    },
    "StationID": {
      "examples": [
        60000001
      ],
      "format": "int64",
      "type": "integer",
      "x-common-model": "true"
    },
    "ErrorDetail": {
      "properties": {
        "location": {
          "description": "Where the error occurred, e.g. 'body.items[3].tags' or 'path.thing-id'",
          "type": "string"
        },
        "message": {
          "description": "Error message text",
          "type": "string"
        },
        "value": {
          "description": "The value at the given location"
        }
      },
      "type": "object"
    },
    "ItemID": {
      "examples": [
        1000000000001
      ],
      "format": "int64",
      "type": "integer",
      "x-common-model": "true"
    }
  },
  "security_schemes": {
    "OAuth2": {
      "flows": {
        "authorizationCode": {
          "authorizationUrl": "https://login.eveonline.com/v2/oauth/authorize",
          "scopes": {
            "esi-access.read_lists.v1": "esi-access.read_lists.v1",
            "esi-activities.read_character.v1": "esi-activities.read_character.v1",
            "esi-alliances.read_contacts.v1": "esi-alliances.read_contacts.v1",
            "esi-assets.read_assets.v1": "esi-assets.read_assets.v1",
            "esi-assets.read_corporation_assets.v1": "esi-assets.read_corporation_assets.v1",
            "esi-calendar.read_calendar_events.v1": "esi-calendar.read_calendar_events.v1",
            "esi-calendar.respond_calendar_events.v1": "esi-calendar.respond_calendar_events.v1",
            "esi-characters.read_agents_research.v1": "esi-characters.read_agents_research.v1",
            "esi-characters.read_blueprints.v1": "esi-characters.read_blueprints.v1",
            "esi-characters.read_contacts.v1": "esi-characters.read_contacts.v1",
            "esi-characters.read_corporation_roles.v1": "esi-characters.read_corporation_roles.v1",
            "esi-characters.read_fatigue.v1": "esi-characters.read_fatigue.v1",
            "esi-characters.read_freelance_jobs.v1": "esi-characters.read_freelance_jobs.v1",
            "esi-characters.read_fw_stats.v1": "esi-characters.read_fw_stats.v1",
            "esi-characters.read_loyalty.v1": "esi-characters.read_loyalty.v1",
            "esi-characters.read_medals.v1": "esi-characters.read_medals.v1",
            "esi-characters.read_notifications.v1": "esi-characters.read_notifications.v1",
            "esi-characters.read_standings.v1": "esi-characters.read_standings.v1",
            "esi-characters.read_titles.v1": "esi-characters.read_titles.v1",
            "esi-characters.write_contacts.v1": "esi-characters.write_contacts.v1",
            "esi-clones.read_clones.v1": "esi-clones.read_clones.v1",
            "esi-clones.read_implants.v1": "esi-clones.read_implants.v1",
            "esi-contracts.read_character_contracts.v1": "esi-contracts.read_character_contracts.v1",
            "esi-contracts.read_corporation_contracts.v1": "esi-contracts.read_corporation_contracts.v1",
            "esi-corporations.read_blueprints.v1": "esi-corporations.read_blueprints.v1",
            "esi-corporations.read_contacts.v1": "esi-corporations.read_contacts.v1",
            "esi-corporations.read_container_logs.v1": "esi-corporations.read_container_logs.v1",
            "esi-corporations.read_corporation_membership.v1": "esi-corporations.read_corporation_membership.v1",
            "esi-corporations.read_divisions.v1": "esi-corporations.read_divisions.v1",
            "esi-corporations.read_facilities.v1": "esi-corporations.read_facilities.v1",
            "esi-corporations.read_freelance_jobs.v1": "esi-corporations.read_freelance_jobs.v1",
            "esi-corporations.read_fw_stats.v1": "esi-corporations.read_fw_stats.v1",
            "esi-corporations.read_medals.v1": "esi-corporations.read_medals.v1",
            "esi-corporations.read_projects.v1": "esi-corporations.read_projects.v1",
            "esi-corporations.read_standings.v1": "esi-corporations.read_standings.v1",
            "esi-corporations.read_starbases.v1": "esi-corporations.read_starbases.v1",
            "esi-corporations.read_structures.v1": "esi-corporations.read_structures.v1",
            "esi-corporations.read_titles.v1": "esi-corporations.read_titles.v1",
            "esi-corporations.track_members.v1": "esi-corporations.track_members.v1",
            "esi-fittings.read_fittings.v1": "esi-fittings.read_fittings.v1",
            "esi-fittings.write_fittings.v1": "esi-fittings.write_fittings.v1",
            "esi-fleets.read_fleet.v1": "esi-fleets.read_fleet.v1",
            "esi-fleets.write_fleet.v1": "esi-fleets.write_fleet.v1",
            "esi-industry.read_character_jobs.v1": "esi-industry.read_character_jobs.v1",
            "esi-industry.read_character_mining.v1": "esi-industry.read_character_mining.v1",
            "esi-industry.read_corporation_jobs.v1": "esi-industry.read_corporation_jobs.v1",
            "esi-industry.read_corporation_mining.v1": "esi-industry.read_corporation_mining.v1",
            "esi-killmails.read_corporation_killmails.v1": "esi-killmails.read_corporation_killmails.v1",
            "esi-killmails.read_killmails.v1": "esi-killmails.read_killmails.v1",
            "esi-location.read_location.v1": "esi-location.read_location.v1",
            "esi-location.read_online.v1": "esi-location.read_online.v1",
            "esi-location.read_ship_type.v1": "esi-location.read_ship_type.v1",
            "esi-mail.organize_mail.v1": "esi-mail.organize_mail.v1",
            "esi-mail.read_mail.v1": "esi-mail.read_mail.v1",
            "esi-mail.send_mail.v1": "esi-mail.send_mail.v1",
            "esi-markets.read_character_orders.v1": "esi-markets.read_character_orders.v1",
            "esi-markets.read_corporation_orders.v1": "esi-markets.read_corporation_orders.v1",
            "esi-markets.structure_markets.v1": "esi-markets.structure_markets.v1",
            "esi-planets.manage_planets.v1": "esi-planets.manage_planets.v1",
            "esi-planets.read_customs_offices.v1": "esi-planets.read_customs_offices.v1",
            "esi-search.search_structures.v1": "esi-search.search_structures.v1",
            "esi-skills.read_skillqueue.v1": "esi-skills.read_skillqueue.v1",
            "esi-skills.read_skills.v1": "esi-skills.read_skills.v1",
            "esi-structures.read_character.v1": "esi-structures.read_character.v1",
            "esi-structures.read_corporation.v1": "esi-structures.read_corporation.v1",
            "esi-ui.open_window.v1": "esi-ui.open_window.v1",
            "esi-ui.write_waypoint.v1": "esi-ui.write_waypoint.v1",
            "esi-universe.read_structures.v1": "esi-universe.read_structures.v1",
            "esi-wallet.read_character_wallet.v1": "esi-wallet.read_character_wallet.v1",
            "esi-wallet.read_corporation_wallets.v1": "esi-wallet.read_corporation_wallets.v1",
            "esi.activity.char:read": "esi.activity.char:read",
            "esi.cosmetic.char:read": "esi.cosmetic.char:read"
          },
          "tokenUrl": "https://login.eveonline.com/v2/oauth/token"
        }
      },
      "type": "oauth2"
    }
  },
  "all_path_names": [
    "/alliances",
    "/alliances/{alliance_id}",
    "/alliances/{alliance_id}/contacts",
    "/alliances/{alliance_id}/contacts/labels",
    "/alliances/{alliance_id}/corporations",
    "/alliances/{alliance_id}/icons",
    "/characters/affiliation",
    "/characters/{character_id}",
    "/characters/{character_id}/access-lists",
    "/characters/{character_id}/access-lists/{access_list_id}",
    "/characters/{character_id}/agents_research",
    "/characters/{character_id}/assets",
    "/characters/{character_id}/assets/locations",
    "/characters/{character_id}/assets/names",
    "/characters/{character_id}/attributes",
    "/characters/{character_id}/blueprints",
    "/characters/{character_id}/calendar",
    "/characters/{character_id}/calendar/{event_id}",
    "/characters/{character_id}/calendar/{event_id}/attendees",
    "/characters/{character_id}/clones",
    "/characters/{character_id}/contacts",
    "/characters/{character_id}/contacts/labels",
    "/characters/{character_id}/contracts",
    "/characters/{character_id}/contracts/{contract_id}/bids",
    "/characters/{character_id}/contracts/{contract_id}/items",
    "/characters/{character_id}/corporationhistory",
    "/characters/{character_id}/cosmetics/skinr",
    "/characters/{character_id}/cosmetics/skinr/components",
    "/characters/{character_id}/cspa",
    "/characters/{character_id}/fatigue",
    "/characters/{character_id}/fittings",
    "/characters/{character_id}/fittings/{fitting_id}",
    "/characters/{character_id}/fleet",
    "/characters/{character_id}/freelance-jobs",
    "/characters/{character_id}/freelance-jobs/{job_id}/participation",
    "/characters/{character_id}/fw/stats",
    "/characters/{character_id}/implants",
    "/characters/{character_id}/industry/jobs",
    "/characters/{character_id}/killmails/recent",
    "/characters/{character_id}/location",
    "/characters/{character_id}/loyalty/points",
    "/characters/{character_id}/mail",
    "/characters/{character_id}/mail/labels",
    "/characters/{character_id}/mail/labels/{label_id}",
    "/characters/{character_id}/mail/lists",
    "/characters/{character_id}/mail/{mail_id}",
    "/characters/{character_id}/medals",
    "/characters/{character_id}/mercenary-tactical-operations",
    "/characters/{character_id}/mercenary-tactical-operations/{operation_id}",
    "/characters/{character_id}/military-campaigns/objectives",
    "/characters/{character_id}/military-campaigns/objectives/{objective_id}",
    "/characters/{character_id}/mining",
    "/characters/{character_id}/notifications",
    "/characters/{character_id}/notifications/contacts",
    "/characters/{character_id}/online",
    "/characters/{character_id}/orders",
    "/characters/{character_id}/orders/history",
    "/characters/{character_id}/paragon-hub/skinr",
    "/characters/{character_id}/planets",
    "/characters/{character_id}/planets/{planet_id}",
    "/characters/{character_id}/portrait",
    "/characters/{character_id}/roles",
    "/characters/{character_id}/search",
    "/characters/{character_id}/ship",
    "/characters/{character_id}/skillqueue",
    "/characters/{character_id}/skills",
    "/characters/{character_id}/standings",
    "/characters/{character_id}/structures/mercenary-dens",
    "/characters/{character_id}/structures/mercenary-dens/{mercenary_den_id}",
    "/characters/{character_id}/titles",
    "/characters/{character_id}/wallet",
    "/characters/{character_id}/wallet/journal",
    "/characters/{character_id}/wallet/transactions",
    "/contracts/public/bids/{contract_id}",
    "/contracts/public/items/{contract_id}",
    "/contracts/public/{region_id}",
    "/corporation/{corporation_id}/mining/extractions",
    "/corporation/{corporation_id}/mining/observers",
    "/corporation/{corporation_id}/mining/observers/{observer_id}",
    "/corporations/npccorps",
    "/corporations/{corporation_id}",
    "/corporations/{corporation_id}/alliancehistory",
    "/corporations/{corporation_id}/assets",
    "/corporations/{corporation_id}/assets/locations",
    "/corporations/{corporation_id}/assets/names",
    "/corporations/{corporation_id}/blueprints",
    "/corporations/{corporation_id}/contacts",
    "/corporations/{corporation_id}/contacts/labels",
    "/corporations/{corporation_id}/containers/logs",
    "/corporations/{corporation_id}/contracts",
    "/corporations/{corporation_id}/contracts/{contract_id}/bids",
    "/corporations/{corporation_id}/contracts/{contract_id}/items",
    "/corporations/{corporation_id}/customs_offices",
    "/corporations/{corporation_id}/divisions",
    "/corporations/{corporation_id}/facilities",
    "/corporations/{corporation_id}/freelance-jobs",
    "/corporations/{corporation_id}/freelance-jobs/{job_id}/participants",
    "/corporations/{corporation_id}/fw/stats",
    "/corporations/{corporation_id}/icons",
    "/corporations/{corporation_id}/industry/jobs",
    "/corporations/{corporation_id}/killmails/recent",
    "/corporations/{corporation_id}/medals",
    "/corporations/{corporation_id}/medals/issued",
    "/corporations/{corporation_id}/members",
    "/corporations/{corporation_id}/members/limit",
    "/corporations/{corporation_id}/members/titles",
    "/corporations/{corporation_id}/membertracking",
    "/corporations/{corporation_id}/orders",
    "/corporations/{corporation_id}/orders/history",
    "/corporations/{corporation_id}/projects",
    "/corporations/{corporation_id}/projects/{project_id}",
    "/corporations/{corporation_id}/projects/{project_id}/contribution/{character_id}",
    "/corporations/{corporation_id}/projects/{project_id}/contributors",
    "/corporations/{corporation_id}/roles",
    "/corporations/{corporation_id}/roles/history",
    "/corporations/{corporation_id}/shareholders",
    "/corporations/{corporation_id}/standings",
    "/corporations/{corporation_id}/starbases",
    "/corporations/{corporation_id}/starbases/{starbase_id}",
    "/corporations/{corporation_id}/structures",
    "/corporations/{corporation_id}/structures/skyhooks",
    "/corporations/{corporation_id}/structures/skyhooks/{skyhook_id}",
    "/corporations/{corporation_id}/structures/sovereignty-hubs",
    "/corporations/{corporation_id}/structures/sovereignty-hubs/{sovereignty_hub_id}",
    "/corporations/{corporation_id}/titles",
    "/corporations/{corporation_id}/wallets",
    "/corporations/{corporation_id}/wallets/{division}/journal",
    "/corporations/{corporation_id}/wallets/{division}/transactions",
    "/cosmetics/skinr/{skinr_id}",
    "/dogma/attributes",
    "/dogma/attributes/{attribute_id}",
    "/dogma/dynamic/items/{type_id}/{item_id}",
    "/dogma/effects",
    "/dogma/effects/{effect_id}",
    "/fleets/{fleet_id}",
    "/fleets/{fleet_id}/members",
    "/fleets/{fleet_id}/members/{member_id}",
    "/fleets/{fleet_id}/squads/{squad_id}",
    "/fleets/{fleet_id}/wings",
    "/fleets/{fleet_id}/wings/{wing_id}",
    "/fleets/{fleet_id}/wings/{wing_id}/squads",
    "/freelance-jobs",
    "/freelance-jobs/{job_id}",
    "/fw/leaderboards",
    "/fw/leaderboards/characters",
    "/fw/leaderboards/corporations",
    "/fw/stats",
    "/fw/systems",
    "/fw/wars",
    "/incursions",
    "/industry/facilities",
    "/industry/systems",
    "/insurance/prices",
    "/killmails/{killmail_id}/{killmail_hash}",
    "/loyalty/stores/{corporation_id}/offers",
    "/markets/groups",
    "/markets/groups/{market_group_id}",
    "/markets/prices",
    "/markets/structures/{structure_id}",
    "/markets/{region_id}/history",
    "/markets/{region_id}/orders",
    "/markets/{region_id}/types",
    "/meta/changelog",
    "/meta/compatibility-dates",
    "/meta/name",
    "/meta/status",
    "/military-campaigns",
    "/military-campaigns/{campaign_id}",
    "/military-campaigns/{campaign_id}/objectives",
    "/military-campaigns/{campaign_id}/objectives/{objective_id}",
    "/paragon-hub/skinr",
    "/paragon-hub/skinr/alliances/{alliance_id}",
    "/paragon-hub/skinr/characters/{character_id}",
    "/paragon-hub/skinr/corporations/{corporation_id}",
    "/route/{origin_system_id}/{destination_system_id}",
    "/skyhooks/raidable",
    "/sovereignty/campaigns",
    "/sovereignty/systems",
    "/status",
    "/ui/autopilot/waypoint",
    "/ui/openwindow/contract",
    "/ui/openwindow/information",
    "/ui/openwindow/marketdetails",
    "/ui/openwindow/newmail",
    "/universe/ancestries",
    "/universe/asteroid_belts/{asteroid_belt_id}",
    "/universe/bloodlines",
    "/universe/categories",
    "/universe/categories/{category_id}",
    "/universe/constellations",
    "/universe/constellations/{constellation_id}",
    "/universe/factions",
    "/universe/graphics",
    "/universe/graphics/{graphic_id}",
    "/universe/groups",
    "/universe/groups/{group_id}",
    "/universe/ids",
    "/universe/moons/{moon_id}",
    "/universe/names",
    "/universe/planets/{planet_id}",
    "/universe/races",
    "/universe/regions",
    "/universe/regions/{region_id}",
    "/universe/schematics/{schematic_id}",
    "/universe/stargates/{stargate_id}",
    "/universe/stars/{star_id}",
    "/universe/stations/{station_id}",
    "/universe/structures",
    "/universe/structures/{structure_id}",
    "/universe/system_jumps",
    "/universe/system_kills",
    "/universe/systems",
    "/universe/systems/{system_id}",
    "/universe/types",
    "/universe/types/{type_id}",
    "/wars",
    "/wars/{war_id}",
    "/wars/{war_id}/killmails"
  ],
  "oauth_discovery": {
    "issuer": "https://login.eveonline.com",
    "authorization_endpoint": "https://login.eveonline.com/v2/oauth/authorize",
    "token_endpoint": "https://login.eveonline.com/v2/oauth/token",
    "userinfo_endpoint": "https://login.eveonline.com/v2/oauth/verify",
    "response_types_supported": [
      "code",
      "token"
    ],
    "jwks_uri": "https://login.eveonline.com/oauth/jwks",
    "revocation_endpoint": "https://login.eveonline.com/v2/oauth/revoke",
    "subject_types_supported": [
      "public"
    ],
    "revocation_endpoint_auth_methods_supported": [
      "client_secret_basic",
      "client_secret_post",
      "client_secret_jwt"
    ],
    "token_endpoint_auth_methods_supported": [
      "client_secret_basic",
      "client_secret_post",
      "client_secret_jwt"
    ],
    "id_token_signing_alg_values_supported": [
      "HS256"
    ],
    "token_endpoint_auth_signing_alg_values_supported": [
      "HS256"
    ],
    "code_challenge_methods_supported": [
      "S256"
    ]
  },
  "receipts": [
    {
      "url": "https://esi.evetech.net/meta/compatibility-dates",
      "retrieved_at": "2026-11-02T15:49:01.061611+00:00",
      "sha256": "7ac78423fb677a08e0edaac0c8fb71e3a70a6abb1e98071fddc45a4aad61e299",
      "etag": null,
      "last_modified": null,
      "bytes": 208
    },
    {
      "url": "https://esi.evetech.net/meta/openapi.json?compatibility_date=2026-08-18",
      "retrieved_at": "2026-11-02T15:49:01.330345+00:00",
      "sha256": "9a9a0f4af77216300e960cfd2576c9baac085a8170022e40c928c28622d80fc6",
      "etag": null,
      "last_modified": null,
      "bytes": 614672
    },
    {
      "url": "https://login.eveonline.com/.well-known/oauth-authorization-server",
      "retrieved_at": "2026-11-02T15:49:01.485329+00:00",
      "sha256": "dc04adbd7e6c74e1e6c3e50efa20a0bd7814bef66a04ec6526f8ce3fe16eb572",
      "etag": null,
      "last_modified": null,
      "bytes": 813
    }
  ],
  "limitations": "Public metadata snapshot only. No authenticated/player route called. Absence from this path inventory is not proof of absence from all CCP services. Revalidate schemas/headers against the selected compatibility date before implementation."
}
```

## Evidence limits
Public commit pins and HTTP snapshot hashes establish what was fetched, not that an implementation is secure or works. Root MIT notices do not settle transitive licences, assets, game-data rights or the separate CCP developer agreement. The official agreement is at https://developers.eveonline.com/license-agreement and requires an owner review; no agreement was accepted and no commercial/ISK model is approved by this packet.
