---
title: "Create"
linkTitle: "Create"
weight: 5
description: >
  Learn how to create a repo.
---

## Endpoint

```
POST /api/v1/repos
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
}
```
