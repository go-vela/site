---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a user.
---

## Endpoint

```
GET  /api/v1/users/:user
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description  |
| ------ | ------------ |
| `user` | name of user |

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

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/users/OctoKitty"
```

#### Response

```json
{
  "id": 1,
  "name": "OctoKitty",
  "token": null,
  "favorites": ["github/octocat"],
  "active": true,
  "admin": false
}
```
