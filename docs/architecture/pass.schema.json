{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://github.com/RashedulHaqueRonjon/PASS-Framework/blob/main/docs/architecture/pass.schema.json",
  "title": "PASS project configuration",
  "description": "Version 1 project-scoped PASS configuration. This file contains no credentials or connection-string secrets.",
  "type": "object",
  "additionalProperties": false,
  "required": [
    "schemaVersion",
    "database",
    "ui",
    "features",
    "generation"
  ],
  "properties": {
    "schemaVersion": {
      "const": 1
    },
    "database": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "provider",
        "sourceOfTruth",
        "defaultSchema",
        "connectionStringName"
      ],
      "properties": {
        "provider": {
          "const": "SqlServer"
        },
        "sourceOfTruth": {
          "const": "databaseFirst"
        },
        "defaultSchema": {
          "type": "string",
          "minLength": 1
        },
        "connectionStringName": {
          "type": "string",
          "minLength": 1
        },
        "includeSchemas": {
          "type": "array",
          "items": {
            "type": "string",
            "minLength": 1
          },
          "uniqueItems": true
        },
        "excludeObjects": {
          "type": "array",
          "items": {
            "type": "string",
            "minLength": 1
          },
          "uniqueItems": true
        }
      }
    },
    "ui": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "cssFramework",
        "theme",
        "layout",
        "gridProvider"
      ],
      "properties": {
        "cssFramework": {
          "enum": [
            "Bootstrap5",
            "None",
            "Existing"
          ]
        },
        "theme": {
          "enum": [
            "light",
            "dark",
            "system",
            "existing"
          ]
        },
        "layout": {
          "enum": [
            "existing",
            "sidebar",
            "topNavigation",
            "none"
          ]
        },
        "gridProvider": {
          "enum": [
            "native",
            "syncfusion",
            "other",
            "none"
          ]
        }
      }
    },
    "features": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "pagination",
        "search",
        "sorting",
        "ajaxCrud",
        "validation",
        "auditTrail",
        "softDelete",
        "antiForgery"
      ],
      "properties": {
        "pagination": {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "enabled",
            "mode",
            "pageSize"
          ],
          "properties": {
            "enabled": {
              "type": "boolean"
            },
            "mode": {
              "enum": [
                "server",
                "client"
              ]
            },
            "pageSize": {
              "type": "integer",
              "minimum": 1,
              "maximum": 500
            }
          }
        },
        "search": {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "enabled",
            "global",
            "column"
          ],
          "properties": {
            "enabled": {
              "type": "boolean"
            },
            "global": {
              "type": "boolean"
            },
            "column": {
              "type": "boolean"
            }
          }
        },
        "sorting": {
          "type": "object",
          "additionalProperties": false,
          "required": [
            "enabled",
            "mode"
          ],
          "properties": {
            "enabled": {
              "type": "boolean"
            },
            "mode": {
              "enum": [
                "allowlisted"
              ]
            }
          }
        },
        "ajaxCrud": {
          "type": "boolean"
        },
        "validation": {
          "enum": [
            "DataAnnotations",
            "FluentValidation",
            "Existing"
          ]
        },
        "auditTrail": {
          "type": "boolean"
        },
        "softDelete": {
          "type": "boolean"
        },
        "antiForgery": {
          "const": true
        }
      }
    },
    "generation": {
      "type": "object",
      "additionalProperties": false,
      "required": [
        "defaultMode",
        "requireApprovalToPrepare",
        "requireApprovalToApply",
        "conflictPolicy",
        "manifestPath",
        "baselinePath",
        "allowDatabaseWrites"
      ],
      "properties": {
        "defaultMode": {
          "const": "planOnly"
        },
        "requireApprovalToPrepare": {
          "const": true
        },
        "requireApprovalToApply": {
          "const": true
        },
        "conflictPolicy": {
          "const": "stopAndReport"
        },
        "manifestPath": {
          "type": "string",
          "minLength": 1
        },
        "baselinePath": {
          "type": "string",
          "minLength": 1
        },
        "allowDatabaseWrites": {
          "const": false
        }
      }
    }
  }
}
