---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list hooks.
---

## Endpoint

```
GET  /api/v1/hooks/:org/:repo
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |

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

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/hooks/github/octocat"
```

#### Response

```json
[
  {
    "id": 2,
    "repo_id": 1,
    "build_id": 1,
    "number": 2,
    "source_id": "c8da1302-07d6-11ea-882f-4893bca275b8",
    "created": "1563474076",
    "host": "github.com",
    "event": "push",
    "branch": "main",
    "error": "",
    "status": "success",
    "link": ""
  },
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
    "status": "success",
    "link": ""
  }
]
```
