---
title: "List"
linkTitle: "List"
description: >
  Learn how to list your dashboards.
---

## Endpoint

```
GET  /api/v1/user/dashboards
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | indicates a bad request                             |
| `401`       | indicates the user does not have proper permissions |
| `404`       | indicates the resource does not exist               |
| `500`       | indicates a server error                            |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/user/dashboards"
```

#### Response

```json
[
  {
    "dashboard": {
      "id": "215d0834-a08a-4203-aee5-542681c4dc8d",
      "name": "Friends",
      "created_at": 1718118753,
      "created_by": "Octocat",
      "updated_at": 1718120350,
      "updated_by": "OctoKitty",
      "admins": [
        {
          "id": 287,
          "name": "OctoKitty",
          "active": true
        },
        {
          "id": 126,
          "name": "Octocat",
          "active": true
        }
      ],
      "repos": [
        {
          "id": 293,
          "name": "Octocat/myvela"
        },
        {
          "id": 34,
          "name": "OctoPal/heyvela"
        }
      ]
    },
    "repos": [
      // repo build information
    ]
  },
  {
    "dashboard": {
      "id": "3e84cf64-4730-4067-bdbc-6961e37a3a92",
      "name": "test",
      "created_at": 1721254450,
      "created_by": "Octocat",
      "updated_at": 1721254596,
      "updated_by": "Octocat",
      "admins": [
        {
          "id": 126,
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
    },
    "repos": [
      // repo build information
    ]
  }
]
```