---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a secret.
---

## Endpoint

```
POST  /api/v1/secrets/:engine/:type/:org/:name
```

## Parameters

The following parameters are used to configure the endpoint:

| Name     | Description                  |
| -------- | ---------------------------- |
| `engine` | name of engine               |
| `type`   | name of type of secret       |
| `org`    | name of organization         |
| `name`   | name of repository or team   |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Sample

#### File

```json
{
  "name": "foo",
  "value": "bar",
  "images": ["alpine"],
  "events": ["push"]
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json"
  "http://127.0.0.1:8080/api/v1/secrets/native/repo/github/octocat"
```

#### Response

```json
{
  "id": 1,
  "org": "github",
  "repo": "octocat",
  "team": "",
  "name": "foo",
  "value": null,
  "type": "repo",
  "images": [
    "alpine"
  ],
  "events": [
    "push"
  ]
}
```
