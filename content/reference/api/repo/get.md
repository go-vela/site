---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list repos by current user or by organization.
---

## Endpoint

```
GET  /api/v1/repos
```
This will return a list of all repos owned by the user.

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
    "allow_tag": false,
    "allow_comment": false,
    "pipeline_type": "yaml"
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
    "allow_tag": false,
    "allow_comment": false,
    "pipeline_type": "yaml"
  }
]
```

## Endpoint

```
GET  /api/v1/repos/:org
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |

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
  "http://127.0.0.1:8080/api/v1/repos/octocat"
```

#### Response

```json
[
  {
    "id": 1,
    "user_id": 1,
    "org": "octocat",
    "name": "example",
    "full_name": "octocat/example",
    "link": "https://github.com/octocat/example",
    "clone": "https://github.com/octocat/example.git",
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
    "allow_tag": false,
    "allow_comment": false,
    "pipeline_type": "yaml"
  },
  {
    "id": 2,
    "user_id": 1,
    "org": "octocat",
    "name": "octokitty",
    "full_name": "octocat/octokitty",
    "link": "https://github.com/octocat/octokitty",
    "clone": "https://github.com/octocat/octokitty.git",
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
    "allow_tag": false,
    "allow_comment": false,
    "pipeline_type": "yaml"
  }
]
```