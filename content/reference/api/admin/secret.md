---
title: "Secret"
linkTitle: "Secret"
description: >
  Learn how to update a secret as an admin in the system.
---

## Endpoint

```
GET  /api/v1/admin/secret
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

Note: You must provide the entire secret object, as this endpoint overwrites the
existing entry for the secret.

#### File

```json
{
  "id": 1,
  "org": "github",
  "repo": "octocat",
  "team": "",
  "name": "foo",
  "value": "",
  "type": "repo",
  "images": ["alpine"],
  "events": ["push", "tag"],
  "allow_command": true,
  "allow_substitution": true,
  "allow_events": {
    "push": {
      "branch": true,
      "tag": true,
      "delete_branch": false,
      "delete_tag": false
    },
    "pull_request": {
      "opened": false,
      "edited": false,
      "synchronize": false,
      "reopened": false
    },
    "deployment": {
      "created": true
    },
    "comment": {
      "created": false,
      "edited": false
    },
    "schedule": {
      "run": false
    }
  },
  "created_at": 1641314085,
  "created_by": "octokitty",
  "updated_at": 1641314500,
  "updated_by": "octocat"
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json"
  "http://127.0.0.1:8080/api/v1/admin/secret"
```

#### Response

```json
{
  "id": 1,
  "org": "github",
  "repo": "octocat",
  "team": "",
  "name": "foo",
  "value": "",
  "type": "repo",
  "images": ["alpine"],
  "events": ["push", "tag"],
  "allow_command": true,
  "allow_substitution": true,
  "allow_events": {
    "push": {
      "branch": true,
      "tag": true,
      "delete_branch": false,
      "delete_tag": false
    },
    "pull_request": {
      "opened": false,
      "edited": false,
      "synchronize": false,
      "reopened": false
    },
    "deployment": {
      "created": true
    },
    "comment": {
      "created": false,
      "edited": false
    },
    "schedule": {
      "run": false
    }
  },
  "created_at": 1641314085,
  "created_by": "octokitty",
  "updated_at": 1641314500,
  "updated_by": "octocat"
}
```
