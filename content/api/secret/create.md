---
title: "Create"
linkTitle: "Create"
weight: 5
description: >
  Learn how to create a secret.
---

## Endpoint

```
POST /api/v1/secrets/:engine/:type/:org/:name
```

| Param | Description |
|---|---|
| engine | Name of engine. |
| type | Name of type. |
| org | Name of organization. |
| name | Name of repository or team. |

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
	"org": "github",
	"repo": "octocat",
	"team": "",
	"name": "foo",
	"value": "",
	"type": "repo",
	"images": [
		"alpine"
	],
	"events": [
		"push"
	]
}
```
