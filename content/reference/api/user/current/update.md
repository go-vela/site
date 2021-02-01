---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify the current user.
---

## Endpoint

```
PUT  /api/v1/user
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
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
  "admin": true
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/user"
```

#### Response

```json
{
  "id": 1,
  "name": "OctoKitty",
  "token": null,
  "favorites": ["github/octocat"],
  "active": true,
  "admin": true
}
```
