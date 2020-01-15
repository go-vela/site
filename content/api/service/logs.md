---
title: "Logs"
linkTitle: "Logs"
weight: 20
description: >
  Learn how to view service logs.
---

## Endpoint

```
GET /api/v1/repos/:org/:repo/builds/:build/services/:service/logs
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
| build | Number of build. |
| service | Number of service. |

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
	"service_id": 1,
	"step_id": 1,
	"data": "SGVsbG8sIFdvcmxkIQ=="
}
```
