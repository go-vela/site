---
title: "Hook"
linkTitle: "Hook"
description: >
  Learn how to update a hook as an admin in the system.
---

## Endpoint

```
PUT  /api/v1/admin/hook
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

Note: You must provide the entire hook object, as this endpoint overwrites the
existing entry for the hook.

#### File

```json
{
  "id": 1,
  "repo_id": 1,
  "build_id": 1,
  "number": 1,
  "source_id": "c8da1302-07d6-11ea-882f-4893bca275b8",
  "created": "1563474076",
  "host": "github.com",
  "event": "push",
  "branch": "main",
  "error": "",
  "status": "failure",
  "link": ""
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/admin/hook"
```

#### Response

```json
{
  "id": 1,
  "repo_id": 1,
  "build_id": 1,
  "number": 1,
  "source_id": "c8da1302-07d6-11ea-882f-4893bca275b8",
  "created": "1563474076",
  "host": "github.com",
  "event": "push",
  "branch": "main",
  "error": "",
  "status": "failure",
  "link": ""
}
```
