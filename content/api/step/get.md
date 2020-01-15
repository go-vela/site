---
title: "Get"
linkTitle: "Get"
weight: 10
description: >
  Learn how to get steps.
---

## Endpoint

```
GET /api/v1/repos/:org/:repo/builds/:build/steps
```

| Param | Description           |
| ----- | --------------------- |
| org   | Name of organization. |
| repo  | Name of repository.   |
| build | Number of build.      |

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description                                          |
| ----------- | ---------------------------------------------------- |
| 200         | Indicates the request has succeeded.                 |
| 401         | Indicates the user does not have proper permissions. |

## Example Response Body

```json
[
  {
    "id": 2,
    "build_id": 1,
    "repo_id": 1,
    "number": 2,
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
