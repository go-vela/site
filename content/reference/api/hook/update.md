---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a hook.
---

## Endpoint

```
PUT  /api/v1/hooks/:org/:repo/:hook
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |
| `hook` | number of hook       |

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

#### File

```json
{
  "status": "failure"
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/hooks/github/octocat/1"
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
  "branch": "master",
  "error": "",
  "status": "failure",
  "link": ""
}
```
