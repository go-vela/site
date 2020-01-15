---
title: "Update"
linkTitle: "Update"
weight: 30
description: >
  Learn how to update a repo.
---

## Endpoint

```
PUT /api/v1/repos/:org/:repo
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
