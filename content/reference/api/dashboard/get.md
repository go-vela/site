---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to get a dashboard.
---

## Endpoint

```
GET  /api/v1/dashboards/:id
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
  "http://127.0.0.1:8080/api/v1/dashboards/3e84cf64-4730-4067-bdbc-6961e37a3a92"
```

#### Response

```json
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
    {
      "org": "Octocat",
      "name": "myvela",
      "counter": 1703,
      "active": true,
      "builds": [
        {
          "number": 1703,
          "started": 1721164234,
          "finished": 1721164240,
          "sender": "Octocat",
          "status": "success",
          "event": "push",
          "branch": "develop",
          "link": "https://http://127.0.0.1:8080/Octocat/myvela/1703"
        },
        {
          "number": 1702,
          "sender": "Octocat",
          "status": "pending approval",
          "event": "pull_request",
          "branch": "main",
          "link": "https://http://127.0.0.1:8080/Octocat/myvela/1702"
        },
        {
          "number": 1701,
          "started": 1721071014,
          "finished": 1721071016,
          "sender": "Octocat",
          "status": "failure",
          "event": "push",
          "branch": "develop",
          "link": "https://http://127.0.0.1:8080/Octocat/myvela/1701"
        },
        {
          "number": 1700,
          "started": 1721070428,
          "finished": 1721070441,
          "sender": "Octocat",
          "status": "failure",
          "event": "push",
          "branch": "develop",
          "link": "https://http://127.0.0.1:8080/Octocat/myvela/1700"
        },
        {
          "number": 1699,
          "started": 1721070363,
          "finished": 1721070375,
          "sender": "Octocat",
          "status": "failure",
          "event": "push",
          "branch": "develop",
          "link": "https://http://127.0.0.1:8080/Octocat/myvela/1699"
        }
      ]
    }
  ]
}
```