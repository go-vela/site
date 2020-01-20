---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a build.
---

## Endpoint

```
DELETE  /api/v1/repos/:org/:repo/builds/:build
```

## Parameters

The following parameters are used to configure the endpoint:

| Name    | Description          |
| ------- | -------------------- |
| `org`   | name of organization |
| `repo`  | name of repository   |
| `build` | number of build      |

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
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/builds/1"
```

#### Response

```sh
build github/octocat/1 removed
```
