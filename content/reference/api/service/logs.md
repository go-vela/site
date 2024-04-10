---
title: "Logs"
linkTitle: "Logs"
description: >
  Learn how to view logs for a service.
---

## Endpoint

```
GET  /api/v1/repos/:org/:repo/builds/:build/services/:service/logs
```

## Parameters

The following parameters are used to configure the endpoint:

| Name      | Description          |
| --------- | -------------------- |
| `org`     | name of organization |
| `repo`    | name of repository   |
| `build`   | number of build      |
| `service` | number of service    |

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

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/builds/1/services/1/logs"
```

#### Response

```json
{
  "id": 1,
  "build_id": 1,
  "repo_id": 1,
  "service_id": 1,
  "data": "SGVsbG8sIFdvcmxkIQ=="
}
```

The `data` field is base64 encoded. To decode the data, you can use the following command:

```sh
echo "SGVsbG8sIFdvcmxkIQ==" | base64 --decode
```
