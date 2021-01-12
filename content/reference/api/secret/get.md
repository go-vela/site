---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list secrets.
---

## Endpoint

```
GET  /api/v1/secrets/:engine/:type/:org/:name
```

## Parameters

The following parameters are used to configure the endpoint:

| Name     | Description                |
| -------- | -------------------------- |
| `engine` | name of engine             |
| `type`   | name of type of secret     |
| `org`    | name of organization       |
| `name`   | name of repository or team |

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
  "http://127.0.0.1:8080/api/v1/secrets/native/repo/github/octocat"
```

#### Response

```json
[
  {
    "id": 1,
    "org": "github",
    "repo": "octocat",
    "team": "",
    "name": "foo",
    "value": null,
    "type": "repo",
    "images": ["alpine"],
    "events": ["push"]
  },
  {
    "id": 2,
    "org": "github",
    "repo": "octocat",
    "team": "",
    "name": "bar",
    "value": null,
    "type": "repo",
    "images": ["alpine"],
    "events": ["push"]
  }
]
```
