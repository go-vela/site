---
title: "Get"
linkTitle: "Get"
weight: 10
description: >
  Learn how to get builds.
---

## Endpoint

```
GET /api/v1/repos/:org/:repo/builds
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description |
|---|---|
| 200 | Indicates the request has succeeded. |
| 401 | Indicates the user does not have proper permissions. |

## Example Response Body

```json
[
	{
		"id": 2,
		"repo_id": 1,
		"number": 2,
		"parent": 1,
		"event": "push",
		"status": "running",
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
	},
	{
		"id": 1,
		"repo_id": 1,
		"number": 1,
		"parent": 1,
		"event": "push",
		"status": "running",
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
```
