---
title: "View"
linkTitle: "View"
description: >
  Learn how to view active platform settings.
---

## Endpoint

```
GET  /api/v1/admin/settings
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                                |
| ----------- | ---------------------------------------------------------- |
| `200`       | indicates the request has succeeded                        |
| `401`       | indicates the user does not have proper permissions        |
| `404`       | indicates the server was unable to retrieve a resource     |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
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
