---
title: "Restart"
linkTitle: "Restart"
description: >
  Learn how to rerun a build.
---

## Endpoint

```
POST  /api/v1/repos/:org/:repo/builds/:build
```

## Parameters

The following parameters are used to configure the endpoint:

| Name    | Description          |
| ------- | -------------------- |
| `org`   | name of organization |
| `repo`  | name of repository   |
| `build` | number of build      |

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

To authenticate to the API, please review the [authentication documentation](/docs/api/authentication).
{{% /alert %}}

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/builds/1"
```

#### Response

```json
{
  "id": 2,
  "repo_id": 1,
  "number": 2,
  "parent": 1,
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
  "host": "company.localhost",
  "runtime": "docker",
  "distribution": "linux"
}
```
