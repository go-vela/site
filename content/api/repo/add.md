---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a repo.
---

## Endpoint

```
POST  /api/v1/repos
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

#### File

```json
{
  "owner": "github",
  "name": "octocat",
  "link": "https://github.com/github/octocat",
  "clone": "https://github.com/github/octocat.git"
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/repos"
```

#### Response

```json
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
}
```
