---
title: "Create"
linkTitle: "Create"
weight: 5
description: >
  Learn how to create a service.
---

## Endpoint

```
POST /api/v1/repos/:org/:repo/builds/:build/services
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
{
	"id": 1,
	"build_id": 1,
	"repo_id": 1,
	"number": 1,
	"name": "clone",
	"status": "success",
	"error": "",
	"exit_code": 0,
	"created": 1563475419,
	"started": 1563475420,
	"finished": 1563475421,
}
```
