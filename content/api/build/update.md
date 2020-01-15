---
title: "Update"
linkTitle: "Update"
weight: 30
description: >
  Learn how to update a build.
---

## Endpoint

```
PUT /api/v1/repos/:org/:repo/builds/:build
```

| Param | Description           |
| ----- | --------------------- |
| org   | Name of organization. |
| repo  | Name of repository.   |
| build | Number of build.      |

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description                                          |
| ----------- | ---------------------------------------------------- |
| 200         | Indicates the request has succeeded.                 |
| 401         | Indicates the user does not have proper permissions. |

## Example Response Body

```json
{
  "id": 1,
  "repo_id": 1,
  "number": 1,
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
