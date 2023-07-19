---
title: "Clean"
linkTitle: "Clean"
description: >
  Learn how to clean dangling resources as an admin in the system.
---

## Endpoint

```
PUT  /api/v1/admin/clean
```

## Filters

The following optional filters are available:

| Name       | Description                                                                                                | 
| --------   | ---------------------------------------------------------------------------------------------------------- |
| `before`   | clean resources created before a certain time (UNIX Epoch, default = "now" minus repo timeout + 5 minutes) |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | indicates bad request                               |
| `401`       | indicates user does not have proper permissions     |
| `500`       | indicates internal server issue while cleaning      |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
  "message": "this resource has been set to error by platform admins during maintenance"
}
```

Note: the default value for `message` is "build cleaned by platform admin"

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/admin/clean"
```

#### Response

```json
  "42 builds cleaned. 42 services cleaned. 42 steps cleaned."
```