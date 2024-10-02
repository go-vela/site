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

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
  "number": 1,
  "source_id": "c8da1302-07d6-11ea-882f-4893bca275b8",
  "host": "github.com",
  "event": "push",
  "branch": "main",
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
  "id": 2,
  "number": 2,
  "source_id": "c8da1302-07d6-11ea-882f-4893bca275b8",
  "created": "1563474076",
  "host": "github.com",
  "event": "push",
  "branch": "main",
  "error": "",
  "status": "success",
  "link": "",
  "repo": {
    "id": 1,
    "user_id": 1,
    "org": "github",
    "name": "octocat",
    "full_name": "github/octocat",
    "link": "https://github.com/github/octocat",
    "clone": "https://github.com/github/octocat.git",
    "branch": "main",
    "build_limit": 10,
    "timeout": 60,
    "counter": 0,
    "visibility": "public",
    "private": false,
    "trusted": true,
    "active": true,
    "allow_pull": true,
    "allow_push": true,
    "allow_deploy": false,
    "allow_tag": false,
    "allow_comment": false,
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
        "reopened": false,
        "labeled": false,
        "unlabeled": false
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
    "pipeline_type": "yaml"
  },
  "build": {
    "id": 10,
    "repo": {
      "id": 1,
    },
    "number": 5,
    "parent": 4,
    "event": "push",
    "status": "created",
    "error": "",
    "enqueued": 1563474204,
    "created": 1563474204,
    "started": 1563474204,
    "finished": 0,
    "deploy": "",
    "clone": "https://github.com/github/octocat.git",
    "source": "https://github.com/github/octocat/commit/48afb5bdc41ad69bf22588491333f7cf71135163",
    "title": "push received from https://github.com/github/octocat",
    "message": "Second commit...",
    "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
    "sender": "OctoKitty",
    "author": "OctoKitty",
    "branch": "main",
    "ref": "refs/heads/main",
    "base_ref": "",
    "host": "ed95dcc0687c",
    "runtime": "",
    "distribution": ""
  }
}
```
