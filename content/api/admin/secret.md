---
title: "Secret"
linkTitle: "Secret"
description: >
  Learn how to list all secrets in the system.
---

## Endpoint

```
GET  /api/v1/admin/secrets
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

To authenticate to the API, please review the [authentication documentation](/docs/api/authentication).
{{% /alert %}}

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/admin/secrets"
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
    "images": [
      "alpine"
    ],
    "events": [
      "push"
    ]
  },
  {
    "id": 2,
    "org": "github",
    "repo": "octocat",
    "team": "",
    "name": "bar",
    "value": null,
    "type": "repo",
    "images": [
      "alpine"
    ],
    "events": [
      "push"
    ]
  }
]
```
