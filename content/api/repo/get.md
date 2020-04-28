---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list repos.
---

## Endpoint

```
GET  /api/v1/repos
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

To authenticate to the API, please review the [authentication documentation](/docs/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/repos"
```

#### Response

```json
[
  {
    "id": 1,
    "user_id": 1,
    "org": "github",
    "name": "octocat",
    "full_name": "github/octocat",
    "link": "https://github.com/github/octocat",
    "clone": "https://github.com/github/octocat.git",
    "branch": "master",
    "timeout": 60,
    "visibility": "public",
    "private": false,
    "trusted": true,
    "active": true,
    "allow_pull": true,
    "allow_push": true,
    "allow_deploy": false,
    "allow_tag": false
  },
  {
    "id": 2,
    "user_id": 1,
    "org": "github",
    "name": "octokitty",
    "full_name": "github/octokitty",
    "link": "https://github.com/github/octokitty",
    "clone": "https://github.com/github/octokitty.git",
    "branch": "master",
    "timeout": 60,
    "visibility": "public",
    "private": false,
    "trusted": true,
    "active": true,
    "allow_pull": true,
    "allow_push": true,
    "allow_deploy": false,
    "allow_tag": false
  }
]
```
