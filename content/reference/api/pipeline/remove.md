---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a pipeline.
---

## Endpoint

```
DELETE  /api/v1/pipelines/:org/:repo/:pipeline
```

## Parameters

The following parameters are used to configure the endpoint:

| Name       | Description                             |
|------------|-----------------------------------------|
| `org`      | name of organization                    |
| `repo`     | name of repository                      |
| `pipeline` | commit SHA for pipeline from repository |

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
  -X DELETE \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat/48afb5bdc41ad69bf22588491333f7cf71135163"
```

#### Response

```sh
Pipeline github/octocat/48afb5bdc41ad69bf22588491333f7cf71135163 deleted
```
