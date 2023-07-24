---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a schedule.
---

## Endpoint

```
PUT  /api/v1/schedules/:org/:repo/:schedule
```

## Parameters

The following parameters are used to configure the endpoint:

| Name       | Description                      |
|------------|----------------------------------|
| `org`      | name of organization             |
| `repo`     | name of repository               |
| `schedule` | name of schedule from repository |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
|-------------|-----------------------------------------------------|
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### File

```json
{
  "active": false
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/schedules/github/octocat/hourly"
```

#### Response

```json
{
  "id": 1,
  "repo_id": 1,
  "active": false,
  "name": "hourly",
  "entry": "0 * * * *",
  "created_at": 1641314085,
  "created_by": "octokitty",
  "updated_at": 1641314086,
  "updated_by": "octokitty",
  "scheduled_at": 0
}
```