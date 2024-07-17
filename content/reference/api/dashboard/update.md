---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to update a dashboard.
---

## Endpoint

```
PUT  /api/v1/dashboards/:id
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
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
    "id": "f460e0a1-a6a5-4724-89e8-4b2b39e12012",
    "name": "new-name",
    "admins": [
        {
            "id": 1,
            "name": "Octocat",
            "active": true
        },
        {
            "name": "MyFriend"
        }
    ],
    "repos": [
        {
            "name": "Octocat/myvela"
        },
        {
            "name": "Octocat/other-repo"
        }
    ]
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/dashboards/f460e0a1-a6a5-4724-89e8-4b2b39e12012"
```

#### Response

```json
{
    "id": "f460e0a1-a6a5-4724-89e8-4b2b39e12012",
    "name": "new-name",
    "created_at": 1721251709,
    "created_by": "Octocat",
    "updated_at": 1721253772,
    "updated_by": "Octocat",
    "admins": [
        {
            "id": 1,
            "name": "Octocat",
            "active": true
        },
        {
            "id": 2,
            "name": "MyFriend",
            "active": true
        }
    ],
    "repos": [
        {
            "id": 293,
            "name": "Octocat/myvela"
        },
        {
            "id": 294,
            "name": "Octocat/other-repo"
        }
    ]
}
```