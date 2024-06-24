---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a repo.
---

## Endpoint

```
POST  /api/v1/repos
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

#### File

```json
{
  "org": "github",
  "name": "octocat",
  "link": "https://github.com/github/octocat",
  "clone": "https://github.com/github/octocat.git"
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/repos"
```

#### Response

```json
{
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
}
```
