---
title: "Chown"
linkTitle: "Chown"
description: >
  Learn how to change ownership of a repo.
---

## Endpoint

```
PATCH  /api/v1/repos/:org/:repo/chown
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |

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
  -X PATCH \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/chown"
```

#### Response

```
Repo github/octocat changed owner
```
