---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a schedule.
---

## Endpoint

```
POST  /api/v1/schedules/:org/:repo
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
|--------|----------------------|
| `org`  | name of organization |
| `repo` | name of repository   |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
|-------------|-----------------------------------------------------|
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
  "name": "hourly",
  "entry": "0 * * * *",
  "active": true
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/schedules/github/octocat"
```

#### Response

```json
{
	"id": 1,
	"repo": {
		"id": 1,
		"owner": {
			"id": 1,
			"name": "octokitty",
			"active": true
		},
		"org": "github",
		"name": "octokitty",
		"full_name": "github/octokitty",
		"link": "https://github.com/github/octokitty",
		"clone": "https://github.com/github/octokitty.git",
		"branch": "main",
		"topics": [],
		"build_limit": 10,
		"timeout": 30,
		"counter": 0,
		"visibility": "public",
		"private": false,
		"trusted": false,
		"active": true,
		"allow_events": {
			"push": {
				"branch": true,
				"tag": false,
				"delete_branch": false,
				"delete_tag": false
			},
			"pull_request": {
				"opened": false,
				"edited": false,
				"synchronize": false,
				"reopened": false,
				"labeled": false,
				"unlabeled": false
			},
			"deployment": {
				"created": false
			},
			"comment": {
				"created": false,
				"edited": false
			},
			"schedule": {
				"run": false
			}
		},
		"pipeline_type": "yaml",
		"previous_name": "",
		"approve_build": "fork-always"
	},
	"active": true,
	"name": "hourly",
	"entry": "0 * * * *",
	"created_at": 1716495910,
	"created_by": "octokitty",
	"updated_at": 1716495910,
	"updated_by": "octokitty",
	"scheduled_at": 0,
	"branch": "main",
	"error": "",
	"next_run": 1716499800
}
```