---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list deployments.
---

## Endpoint

```
GET  /api/v1/deployments/:org/:repo
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
  "http://127.0.0.1:8080/api/v1/deployments/github/octocat"
```

#### Response

```json
[
  {
    "id": 2,
    "repo_id": 1,
    "url": "https://api.github.com/repos/github/octocat/deployments/2",
    "user": "octocat",
    "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
    "ref": "master",
    "task": "deploy:vela",
    "target": "production",
    "description": "Deployment request from Vela",
		"payload": {},
		"builds": [
      {
        "id": 10,
        "repo_id": 1,
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
        "branch": "master",
        "ref": "refs/heads/master",
        "base_ref": "",
        "host": "ed95dcc0687c",
        "runtime": "",
        "distribution": ""
      }
    ]
  },
  {
    "id": 9,
    "repo_id": 1,
    "url": "https://api.github.com/repos/github/octocat/deployments/9",
    "user": "octocat",
    "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
    "ref": "master",
    "task": "deploy:vela",
    "target": "production",
    "description": "Deployment request from Vela",
		"payload": {},
		"builds": [
      {
        "id": 1,
        "repo_id": 1,
        "number": 3,
        "parent": 2,
        "event": "push",
        "status": "created",
        "error": "",
        "enqueued": 1563474077,
        "created": 1563474076,
        "started": 1563474077,
        "finished": 0,
        "deploy": "",
        "clone": "https://github.com/github/octocat.git",
        "source": "https://github.com/github/octocat/commit/48afb5bdc41ad69bf22588491333f7cf71135163",
        "title": "push received from https://github.com/github/octocat",
        "message": "First commit...",
        "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
        "sender": "OctoKitty",
        "author": "OctoKitty",
        "branch": "master",
        "ref": "refs/heads/master",
        "base_ref": "",
        "host": "82823eb770b0",
        "runtime": "",
        "distribution": ""
      }
    ]
  }
]
```
