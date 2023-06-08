---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a schedule.
---

## Endpoint

```
GET  /api/v1/schedules/:org/:repo/:schedule
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
| `400`       | unable to retrieve the schedule                     |
| `401`       | indicates the user does not have proper permissions |
| `404`       | unable to retrieve the schedule                     |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/schedules/github/octocat/hourly"
```

#### Response

```json
{
  "id": 1,
  "repo_id": 1,
  "active": true,
  "name": "hourly",
  "entry": "0 * * * *",
  "created_at": 1641314085,
  "created_by": "octokitty",
  "updated_at": 1641314085,
  "updated_by": "octokitty",
  "scheduled_at": 0
}
```