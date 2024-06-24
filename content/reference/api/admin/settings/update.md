---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to update platform settings.
---

## Endpoint

```
PUT  /api/v1/admin/settings
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                                |
| ----------- | ---------------------------------------------------------- |
| `200`       | indicates the request has succeeded                        |
| `401`       | indicates the user does not have proper permissions        |
| `404`       | indicates the server was unable to retrieve a resource     |
| `500`       | indicates a server failure while processing the request    |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
	"compiler": {
		"clone_image": "target/vela-git:latest",
		"template_depth": 3,
		"starlark_exec_limit": 7500
	},
	"queue": {
		"routes": [
			"vela"
		]
	},
	"repo_allowlist": [
		"*",
	],
	"schedule_allowlist": [
		"github/octocat",
	]
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/admin/settings"
```

#### Response

```json
{
	"id": 1,
	"compiler": {
		"clone_image": "target/vela-git:latest",
		"template_depth": 3,
		"starlark_exec_limit": 7500
	},
	"queue": {
		"routes": [
			"vela"
		]
	},
	"repo_allowlist": [
		"*",
	],
	"schedule_allowlist": [
		"github/octocat",
	],
	"created_at": 1715718878,
	"updated_at": 1715718879,
	"updated_by": "octocat"
}
```
