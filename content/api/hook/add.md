---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a hook.
---

## Endpoint

```
POST  /api/v1/hooks/:org/:repo
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

#### File

```json
{
  "number": 1,
  "source_id": "c8da1302-07d6-11ea-882f-4893bca275b8",
  "host": "github.com",
  "event": "push",
  "branch": "master",
  "status": "success"
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/hooks/github/octocat"
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
  "status": "success",
  "link": ""
}
```
