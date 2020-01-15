---
title: "Logs"
linkTitle: "Logs"
weight: 20
description: >
  Learn how to view build logs.
---

## Endpoint

```
GET /api/v1/repos/:org/:repo/builds/:build/logs
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
| build | Number of build. |

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
		"id": 1,
		"step_id": 1,
		"build_id": 1,
		"repo_id": 1,
		"data": "SGVsbG8sIFdvcmxkIQ=="
	},
	{
		"id": 2,
		"step_id": 2,
		"build_id": 1,
		"repo_id": 1,
		"data": "SGVsbG8sIFdvcmxkIQ=="
	}
]
```
