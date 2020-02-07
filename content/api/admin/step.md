---
title: "Step"
linkTitle: "Step"
description: >
  Learn how to list all steps in the system.
---

## Endpoint

```
GET  /api/v1/admin/steps
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
  "http://127.0.0.1:8080/api/v1/admin/steps"
```

#### Response

```json
[
  {
    "id": 2,
    "build_id": 2,
    "repo_id": 2,
    "number": 1,
    "name": "build",
    "status": "success",
    "error": "",
    "exit_code": 0,
    "created": 1563475419,
    "started": 0,
    "finished": 0,
    "host": "company.localhost",
    "runtime": "docker",
    "distribution": "linux"
  },
  {
    "id": 1,
    "build_id": 1,
    "repo_id": 1,
    "number": 1,
    "name": "clone",
    "status": "success",
    "error": "",
    "exit_code": 0,
    "created": 1563475419,
    "started": 0,
    "finished": 0,
    "host": "company.localhost",
    "runtime": "docker",
    "distribution": "linux"
  }
]
```
