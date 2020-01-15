---
title: "Get"
linkTitle: "Get"
weight: 10
description: >
  Learn how to get repos.
---

## Endpoint

```
GET /api/v1/repos
```

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
		"user_id": 1,
		"org": "github",
		"name": "octocat",
		"full_name": "github/octocat",
		"link": "https://github.com/github/octocat",
		"clone": "https://github.com/github/octocat",
		"branch": "master",
		"timeout": 60,
		"visibility": "public",
		"private": false,
		"trusted": true,
		"active": true,
		"allow_pr": false,
		"allow_push": true,
		"allow_deploy": false,
		"allow_tag": false
	},
	{
		"id": 2,
		"user_id": 1,
		"org": "github",
		"name": "octokitty",
		"full_name": "github/octokitty",
		"link": "https://github.com/github/octokitty",
		"clone": "https://github.com/github/octokitty",
		"branch": "master",
		"timeout": 60,
		"visibility": "public",
		"private": false,
		"trusted": true,
		"active": true,
		"allow_pr": false,
		"allow_push": true,
		"allow_deploy": false,
		"allow_tag": false
	}
]
```
