---
title: "View"
linkTitle: "View"
weight: 15
description: >
  Learn how to view a service.
---

## Endpoint

```
GET /api/v1/repos/:org/:repo/builds/:build/services/:service
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
| build | Number of build. |
| service | Number of service. |


`{soon}` - documentation coming soon

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description |
|---|---|
| 200 | Everything looks good! |

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
