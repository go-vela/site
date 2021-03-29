---
title: "Validate"
linkTitle: "Validate"
description: >
  Learn how to validate a pipeline configuration with templates.
---

## Endpoint

```
POST  /api/v1/pipelines/:org/:repo/validate
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |
| `ref`   | file ref for fetching from the source provider   |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | unable to retrieve or validate the pipeline configuration and templates |
| `401`       | indicates the user does not have proper permissions |
| `404`       | unable to retrieve or validate the pipeline configuration or templates |
| `500`       | system error while retrieving or validating the pipeline configuration templates |

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
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat/validate"
```

#### Response

```
"pipeline is valid"
```