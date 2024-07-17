---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a dashboard.
---

## Endpoint

```
POST  /api/v1/dashboards
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `201`       | indicates the request has succeeded                 |
| `400`       | indicates a bad request                             |
| `401`       | indicates the user does not have proper permissions |
| `500`       | indicates a server error                            |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
    "name": "test",
    "created_at": 1721251709,
    "created_by": "Octocat",
    "updated_at": 1721251709,
    "updated_by": "Octocat",
    "admins": [
        {
            "id": 1,
            "name": "Octocat",
            "active": true
        }
    ],
    "repos": [
        {
            "name": "Octocat/myvela"
        }
    ]
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/dashboards"
```

#### Response

```json
{
    "id": "f460e0a1-a6a5-4724-89e8-4b2b39e12012",
    "name": "test",
    "created_at": 1721251709,
    "created_by": "Octocat",
    "updated_at": 1721253772,
    "updated_by": "Octocat",
    "admins": [
        {
            "id": 1,
            "name": "Octocat",
            "active": true
        }
    ],
    "repos": [
        {
            "id": 293,
            "name": "Octocat/myvela"
        }
    ]
}
```