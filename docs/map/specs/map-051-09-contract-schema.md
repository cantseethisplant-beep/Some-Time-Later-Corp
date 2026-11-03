# Machine-readable P0 Tools contract

Normative JSON Schema Draft 2020-12; validate the operation/result against its named `$defs` entry. This is a specification artifact, not a built API. Semantic time/authorship/authorization/transaction constraints remain in 01..03. Duplicate JSON keys and decompressed size are checked at transport parsing before schema validation.

## Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "urn:some-time-later:wh-tools:contract:1",
  "title": "P0 WhTools v1 structural contracts",
  "$defs": {
    "Create": {
      "type": "object",
      "properties": {
        "requestId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "idempotencyKey": {
          "type": "string",
          "pattern": "^[A-Za-z0-9_-]{16,64}$"
        },
        "intentExpiresAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "systemId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "observedAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "text": {
          "type": "string",
          "minLength": 1,
          "maxLength": 4000
        }
      },
      "required": [
        "requestId",
        "idempotencyKey",
        "intentExpiresAt",
        "systemId",
        "observedAt",
        "text"
      ],
      "additionalProperties": false
    },
    "Edit": {
      "type": "object",
      "properties": {
        "requestId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "idempotencyKey": {
          "type": "string",
          "pattern": "^[A-Za-z0-9_-]{16,64}$"
        },
        "intentExpiresAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "expectedRevision": {
          "type": "integer",
          "minimum": 1,
          "maximum": 9007199254740991
        },
        "text": {
          "type": "string",
          "minLength": 1,
          "maxLength": 4000
        }
      },
      "required": [
        "requestId",
        "idempotencyKey",
        "intentExpiresAt",
        "expectedRevision",
        "text"
      ],
      "additionalProperties": false
    },
    "Delete": {
      "type": "object",
      "properties": {
        "requestId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "idempotencyKey": {
          "type": "string",
          "pattern": "^[A-Za-z0-9_-]{16,64}$"
        },
        "intentExpiresAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "expectedRevision": {
          "type": "integer",
          "minimum": 1,
          "maximum": 9007199254740991
        }
      },
      "required": [
        "requestId",
        "idempotencyKey",
        "intentExpiresAt",
        "expectedRevision"
      ],
      "additionalProperties": false
    },
    "ConsentCommand": {
      "type": "object",
      "properties": {
        "requestId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "idempotencyKey": {
          "type": "string",
          "pattern": "^[A-Za-z0-9_-]{16,64}$"
        },
        "intentExpiresAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "expectedRevision": {
          "type": "integer",
          "minimum": 0,
          "maximum": 9007199254740991
        },
        "enabled": {
          "type": "boolean"
        },
        "expiresAt": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
              "format": "date-time"
            },
            {
              "type": "null"
            }
          ]
        }
      },
      "required": [
        "requestId",
        "idempotencyKey",
        "intentExpiresAt",
        "expectedRevision",
        "enabled",
        "expiresAt"
      ],
      "additionalProperties": false,
      "allOf": [
        {
          "if": {
            "properties": {
              "enabled": {
                "const": false
              }
            }
          },
          "then": {
            "properties": {
              "expiresAt": {
                "type": "null"
              }
            }
          },
          "else": {
            "properties": {
              "expiresAt": {
                "type": "string",
                "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
                "format": "date-time"
              }
            }
          }
        }
      ]
    },
    "GrantCommand": {
      "type": "object",
      "properties": {
        "requestId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "idempotencyKey": {
          "type": "string",
          "pattern": "^[A-Za-z0-9_-]{16,64}$"
        },
        "intentExpiresAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "expectedRevision": {
          "type": "integer",
          "minimum": 0,
          "maximum": 9007199254740991
        },
        "view": {
          "type": "boolean"
        },
        "annotate": {
          "type": "boolean"
        },
        "expiresAt": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
              "format": "date-time"
            },
            {
              "type": "null"
            }
          ]
        }
      },
      "required": [
        "requestId",
        "idempotencyKey",
        "intentExpiresAt",
        "expectedRevision",
        "view",
        "annotate",
        "expiresAt"
      ],
      "additionalProperties": false,
      "allOf": [
        {
          "if": {
            "properties": {
              "annotate": {
                "const": true
              }
            }
          },
          "then": {
            "properties": {
              "view": {
                "const": true
              }
            }
          }
        },
        {
          "if": {
            "properties": {
              "view": {
                "const": false
              },
              "annotate": {
                "const": false
              }
            }
          },
          "then": {
            "properties": {
              "expiresAt": {
                "type": "null"
              }
            }
          },
          "else": {
            "properties": {
              "expiresAt": {
                "type": "string",
                "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
                "format": "date-time"
              }
            }
          }
        }
      ]
    },
    "Annotation": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "instanceId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "mapId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "systemId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "authorId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "kind": {
          "const": "note"
        },
        "effectiveSource": {
          "const": "manual"
        },
        "uncertainty": {
          "const": "reported"
        },
        "observedAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "recordedAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "updatedAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "expiresAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        },
        "revision": {
          "type": "integer",
          "minimum": 1,
          "maximum": 9007199254740991
        },
        "text": {
          "type": "string",
          "minLength": 1,
          "maxLength": 4000
        },
        "createdSequence": {
          "type": "integer",
          "minimum": 1,
          "maximum": 9007199254740991
        }
      },
      "required": [
        "id",
        "instanceId",
        "mapId",
        "systemId",
        "authorId",
        "kind",
        "effectiveSource",
        "uncertainty",
        "observedAt",
        "recordedAt",
        "updatedAt",
        "expiresAt",
        "revision",
        "text",
        "createdSequence"
      ],
      "additionalProperties": false
    },
    "Tombstone": {
      "type": "object",
      "properties": {
        "id": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "revision": {
          "type": "integer",
          "minimum": 1,
          "maximum": 9007199254740991
        },
        "deletedAt": {
          "type": "string",
          "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
          "format": "date-time"
        }
      },
      "required": [
        "id",
        "revision",
        "deletedAt"
      ],
      "additionalProperties": false
    },
    "Consent": {
      "type": "object",
      "properties": {
        "enabled": {
          "type": "boolean"
        },
        "expiresAt": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
              "format": "date-time"
            },
            {
              "type": "null"
            }
          ]
        },
        "revision": {
          "type": "integer",
          "minimum": 0,
          "maximum": 9007199254740991
        }
      },
      "required": [
        "enabled",
        "expiresAt",
        "revision"
      ],
      "additionalProperties": false,
      "allOf": [
        {
          "if": {
            "properties": {
              "enabled": {
                "const": false
              }
            }
          },
          "then": {
            "properties": {
              "expiresAt": {
                "type": "null"
              }
            }
          },
          "else": {
            "properties": {
              "expiresAt": {
                "type": "string",
                "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
                "format": "date-time"
              }
            }
          }
        }
      ]
    },
    "Grant": {
      "type": "object",
      "properties": {
        "targetActorId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "view": {
          "type": "boolean"
        },
        "annotate": {
          "type": "boolean"
        },
        "expiresAt": {
          "anyOf": [
            {
              "type": "string",
              "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
              "format": "date-time"
            },
            {
              "type": "null"
            }
          ]
        },
        "revision": {
          "type": "integer",
          "minimum": 0,
          "maximum": 9007199254740991
        }
      },
      "required": [
        "targetActorId",
        "view",
        "annotate",
        "expiresAt",
        "revision"
      ],
      "additionalProperties": false,
      "allOf": [
        {
          "if": {
            "properties": {
              "annotate": {
                "const": true
              }
            }
          },
          "then": {
            "properties": {
              "view": {
                "const": true
              }
            }
          }
        },
        {
          "if": {
            "properties": {
              "view": {
                "const": false
              },
              "annotate": {
                "const": false
              }
            }
          },
          "then": {
            "properties": {
              "expiresAt": {
                "type": "null"
              }
            }
          },
          "else": {
            "properties": {
              "expiresAt": {
                "type": "string",
                "pattern": "^\\d{4}-\\d{2}-\\d{2}T\\d{2}:\\d{2}:\\d{2}\\.\\d{3}Z$",
                "format": "date-time"
              }
            }
          }
        }
      ]
    },
    "ListResult": {
      "type": "object",
      "properties": {
        "items": {
          "type": "array",
          "maxItems": 100,
          "items": {
            "$ref": "#/$defs/Annotation"
          }
        },
        "nextCursor": {
          "anyOf": [
            {
              "type": "string",
              "minLength": 1,
              "maxLength": 2048,
              "pattern": "^[\\x21-\\x7e]+$"
            },
            {
              "type": "null"
            }
          ]
        }
      },
      "required": [
        "items",
        "nextCursor"
      ],
      "additionalProperties": false
    },
    "Event": {
      "type": "object",
      "properties": {
        "eventId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "sequence": {
          "type": "integer",
          "minimum": 1,
          "maximum": 9007199254740991
        },
        "mapId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "systemId": {
          "type": "integer",
          "minimum": 1,
          "maximum": 2147483647
        },
        "type": {
          "enum": [
            "annotation.changed",
            "annotation.deleted",
            "resync.required"
          ]
        }
      },
      "required": [
        "eventId",
        "sequence",
        "mapId",
        "systemId",
        "type"
      ],
      "additionalProperties": false
    },
    "Error": {
      "type": "object",
      "properties": {
        "requestId": {
          "type": "string",
          "pattern": "^[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}$",
          "format": "uuid"
        },
        "code": {
          "enum": [
            "INVALID_PAYLOAD",
            "INVALID_CURSOR",
            "INVALID_REFERENCE",
            "UNAUTHENTICATED",
            "FORBIDDEN",
            "CONTRIBUTION_DISABLED",
            "ANTIFORGERY_INVALID",
            "ORIGIN_INVALID",
            "NOT_FOUND",
            "CONFLICT",
            "IDEMPOTENCY_CONFLICT",
            "INTENT_EXPIRED",
            "RESULT_EXPIRED",
            "PAYLOAD_TOO_LARGE",
            "UNSUPPORTED_MEDIA_TYPE",
            "RATE_LIMITED",
            "BASE_UNAVAILABLE",
            "STORAGE_UNAVAILABLE",
            "SCHEMA_NOT_READY",
            "INTERNAL_ERROR"
          ]
        },
        "message": {
          "type": "string",
          "maxLength": 200
        },
        "current": {
          "anyOf": [
            {
              "$ref": "#/$defs/Annotation"
            },
            {
              "$ref": "#/$defs/Consent"
            },
            {
              "$ref": "#/$defs/Grant"
            },
            {
              "type": "null"
            }
          ]
        }
      },
      "required": [
        "requestId",
        "code",
        "message",
        "current"
      ],
      "additionalProperties": false,
      "allOf": [
        {
          "if": {
            "properties": {
              "code": {
                "not": {
                  "const": "CONFLICT"
                }
              }
            }
          },
          "then": {
            "properties": {
              "current": {
                "type": "null"
              }
            }
          }
        }
      ]
    }
  }
}
```

## Contract fixtures

Each fixture declares its definition, fixed server clock, layer and expected contract result. Semantic fixture checks are specification oracles, not app runtime tests. Successful request examples assume separate valid session/grant/consent/antiforgery/map conditions.

```json
{
  "fixtures": [
    {
      "id": "valid-Create",
      "definition": "Create",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "valid-Edit",
      "definition": "Edit",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 1,
        "text": "Updated report"
      }
    },
    {
      "id": "valid-Delete",
      "definition": "Delete",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 1
      }
    },
    {
      "id": "valid-ConsentCommand",
      "definition": "ConsentCommand",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 0,
        "enabled": true,
        "expiresAt": "2026-11-04T12:00:00.000Z"
      }
    },
    {
      "id": "valid-GrantCommand",
      "definition": "GrantCommand",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 0,
        "view": true,
        "annotate": false,
        "expiresAt": "2026-11-04T12:00:00.000Z"
      }
    },
    {
      "id": "valid-Annotation",
      "definition": "Annotation",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "id": "00000000-0000-4000-8000-000000000111",
        "instanceId": 7,
        "mapId": 42,
        "systemId": 301,
        "authorId": 123,
        "kind": "note",
        "effectiveSource": "manual",
        "uncertainty": "reported",
        "observedAt": "2026-11-03T12:00:00.000Z",
        "recordedAt": "2026-11-03T12:00:00.000Z",
        "updatedAt": "2026-11-03T12:00:00.000Z",
        "expiresAt": "2027-02-01T12:00:00.000Z",
        "revision": 1,
        "text": "Reported movement; verify before acting.",
        "createdSequence": 1
      }
    },
    {
      "id": "valid-Tombstone",
      "definition": "Tombstone",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "id": "00000000-0000-4000-8000-000000000111",
        "revision": 2,
        "deletedAt": "2026-11-03T12:00:00.000Z"
      }
    },
    {
      "id": "valid-Consent",
      "definition": "Consent",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "enabled": false,
        "expiresAt": null,
        "revision": 0
      }
    },
    {
      "id": "valid-Grant",
      "definition": "Grant",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "targetActorId": 123,
        "view": false,
        "annotate": false,
        "expiresAt": null,
        "revision": 0
      }
    },
    {
      "id": "valid-ListResult",
      "definition": "ListResult",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "items": [
          {
            "id": "00000000-0000-4000-8000-000000000111",
            "instanceId": 7,
            "mapId": 42,
            "systemId": 301,
            "authorId": 123,
            "kind": "note",
            "effectiveSource": "manual",
            "uncertainty": "reported",
            "observedAt": "2026-11-03T12:00:00.000Z",
            "recordedAt": "2026-11-03T12:00:00.000Z",
            "updatedAt": "2026-11-03T12:00:00.000Z",
            "expiresAt": "2027-02-01T12:00:00.000Z",
            "revision": 1,
            "text": "Reported movement; verify before acting.",
            "createdSequence": 1
          }
        ],
        "nextCursor": null
      }
    },
    {
      "id": "valid-Event",
      "definition": "Event",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "eventId": "00000000-0000-4000-8000-000000000111",
        "sequence": 1,
        "mapId": 42,
        "systemId": 301,
        "type": "annotation.changed"
      }
    },
    {
      "id": "valid-Error",
      "definition": "Error",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "code": "FORBIDDEN",
        "message": "Access denied",
        "current": null
      }
    },
    {
      "id": "reject-create-sourceKind",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting.",
        "sourceKind": "core-observation"
      }
    },
    {
      "id": "reject-create-authorId",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting.",
        "authorId": 999
      }
    },
    {
      "id": "reject-create-uncertainty",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting.",
        "uncertainty": "corroborated"
      }
    },
    {
      "id": "reject-create-mapId",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting.",
        "mapId": 43
      }
    },
    {
      "id": "reject-create-instanceId",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting.",
        "instanceId": 8
      }
    },
    {
      "id": "reject-create-url",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting.",
        "url": "https://example.invalid"
      }
    },
    {
      "id": "reject-string-system",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": "301",
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-zero-system",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 0,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-bool-system",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": true,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-large-system",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 2147483648,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-long-text",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    },
    {
      "id": "reject-missing-precision",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-offset-time",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000+00:00",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-bad-uuid",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "not-a-uuid",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-short-key",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "small",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-missing-deadline",
      "definition": "Create",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "reject-edit-zero-revision",
      "definition": "Edit",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 0,
        "text": "Updated report"
      }
    },
    {
      "id": "reject-edit-immutable-observedAt",
      "definition": "Edit",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 1,
        "text": "Updated report",
        "observedAt": "2026-11-03T12:00:00.000Z"
      }
    },
    {
      "id": "reject-consent-disabled-expiry",
      "definition": "ConsentCommand",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 0,
        "enabled": false,
        "expiresAt": "2026-11-04T12:00:00.000Z"
      }
    },
    {
      "id": "reject-grant-annotate-without-view",
      "definition": "GrantCommand",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 0,
        "view": false,
        "annotate": true,
        "expiresAt": "2026-11-04T12:00:00.000Z"
      }
    },
    {
      "id": "reject-event-text",
      "definition": "Event",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "eventId": "00000000-0000-4000-8000-000000000111",
        "sequence": 1,
        "mapId": 42,
        "systemId": 301,
        "type": "annotation.changed",
        "text": "private note"
      }
    },
    {
      "id": "reject-response-forged-source",
      "definition": "Annotation",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "id": "00000000-0000-4000-8000-000000000111",
        "instanceId": 7,
        "mapId": 42,
        "systemId": 301,
        "authorId": 123,
        "kind": "note",
        "effectiveSource": "core-observation",
        "uncertainty": "reported",
        "observedAt": "2026-11-03T12:00:00.000Z",
        "recordedAt": "2026-11-03T12:00:00.000Z",
        "updatedAt": "2026-11-03T12:00:00.000Z",
        "expiresAt": "2027-02-01T12:00:00.000Z",
        "revision": 1,
        "text": "Reported movement; verify before acting.",
        "createdSequence": 1
      }
    },
    {
      "id": "reject-error-private-current",
      "definition": "Error",
      "valid": false,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "code": "FORBIDDEN",
        "message": "Access denied",
        "current": {
          "id": "00000000-0000-4000-8000-000000000111",
          "instanceId": 7,
          "mapId": 42,
          "systemId": 301,
          "authorId": 123,
          "kind": "note",
          "effectiveSource": "manual",
          "uncertainty": "reported",
          "observedAt": "2026-11-03T12:00:00.000Z",
          "recordedAt": "2026-11-03T12:00:00.000Z",
          "updatedAt": "2026-11-03T12:00:00.000Z",
          "expiresAt": "2027-02-01T12:00:00.000Z",
          "revision": 1,
          "text": "Reported movement; verify before acting.",
          "createdSequence": 1
        }
      }
    },
    {
      "id": "valid-error-conflict",
      "definition": "Error",
      "valid": true,
      "layer": "schema",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "code": "CONFLICT",
        "message": "Access denied",
        "current": {
          "id": "00000000-0000-4000-8000-000000000111",
          "instanceId": 7,
          "mapId": 42,
          "systemId": 301,
          "authorId": 123,
          "kind": "note",
          "effectiveSource": "manual",
          "uncertainty": "reported",
          "observedAt": "2026-11-03T12:00:00.000Z",
          "recordedAt": "2026-11-03T12:00:00.000Z",
          "updatedAt": "2026-11-03T12:00:00.000Z",
          "expiresAt": "2027-02-01T12:00:00.000Z",
          "revision": 1,
          "text": "Reported movement; verify before acting.",
          "createdSequence": 1
        }
      }
    },
    {
      "id": "semantic-whitespace",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": " \t\n"
      }
    },
    {
      "id": "semantic-nul",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "hello\u0000"
      }
    },
    {
      "id": "semantic-future",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:05:00.001Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "semantic-too-old",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-08-05T11:59:59.999Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "semantic-expired-intent",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:00:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "semantic-long-intent",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:10:00.001Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "semantic-float-id",
      "definition": "Create",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301.0,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "semantic-consent-expiry",
      "definition": "ConsentCommand",
      "valid": false,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "expectedRevision": 0,
        "enabled": true,
        "expiresAt": "2026-11-03T12:00:59.999Z"
      }
    },
    {
      "id": "semantic-text-boundary",
      "definition": "Create",
      "valid": true,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
      }
    },
    {
      "id": "semantic-future-boundary",
      "definition": "Create",
      "valid": true,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:05:00.000Z",
        "text": "Reported movement; verify before acting."
      }
    },
    {
      "id": "semantic-crlf",
      "definition": "Create",
      "valid": true,
      "layer": "semantic",
      "serverNow": "2026-11-03T12:00:00.000Z",
      "value": {
        "requestId": "00000000-0000-4000-8000-000000000501",
        "idempotencyKey": "tools_note_000501",
        "intentExpiresAt": "2026-11-03T12:05:00.000Z",
        "systemId": 301,
        "observedAt": "2026-11-03T12:00:00.000Z",
        "text": "one\r\ntwo"
      }
    }
  ]
}
```
