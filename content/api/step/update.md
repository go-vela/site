---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a step.
---

## Endpoint

```
PUT  /api/v1/repos/:org/:repo/builds/:build/steps/:step
```

## Parameters

The following parameters are used to configure the endpoint:

| Name    | Description          |
| ------- | -------------------- |
| `org`   | name of organization |
| `repo`  | name of repository   |
| `build` | number of build      |
| `step`  | number of step       |

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

#### File

```json
{
  "status": "failure"
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/builds/1/steps/1"
```

#### Response

```json
{
  "id": 1,
  "build_id": 1,
  "repo_id": 1,
  "number": 1,
  "name": "clone",
  "status": "failure",
  "error": "",
  "exit_code": 0,
  "created": 1563475419,
  "started": 0,
  "finished": 0,
  "host": "company.localhost",
  "runtime": "docker",
  "distribution": "linux"
}
```
