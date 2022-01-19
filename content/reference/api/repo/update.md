---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a repo.
---

## Endpoint

```
PUT  /api/v1/repos/:org/:repo
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

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
  "allow_tag": true
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/repos/github/octocat"
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
  "build_limit": 10,
  "timeout": 60,
  "counter": 0,
  "visibility": "public",
  "private": false,
  "trusted": true,
  "active": true,
  "allow_pull": true,
  "allow_push": true,
  "allow_deploy": false,
  "allow_tag": true,
  "allow_comment": false,
  "pipeline_type": "yaml"
}
```
