---
title: "User"
linkTitle: "User"
description: >
  Learn how to update a user as an admin in the system.
---

## Endpoint

```
GET  /api/v1/admin/user
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

Note: You must provide the entire service object, as this endpoint overwrites the
existing entry for the service.

#### File

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

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/admin/user"
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
