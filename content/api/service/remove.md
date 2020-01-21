---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a service.
---

## Endpoint

```
DELETE  /api/v1/repos/:org/:repo/builds/:build/services/:service
```

## Parameters

The following parameters are used to configure the endpoint:

| Name      | Description          |
| --------- | -------------------- |
| `org`     | name of organization |
| `repo`    | name of repository   |
| `build`   | number of build      |
| `service` | number of service    |

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
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/builds/1/services/1"
```

#### Response

```
Service github/octocat/1/1 deleted
```
