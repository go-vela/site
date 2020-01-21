---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a user.
---

## Endpoint

```
DELETE  /api/v1/users/:user
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

#### Request

```sh
curl \
  -X DELETE \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/users/OctoKitty"
```

#### Response

```sh
User OctoKitty deleted
```
