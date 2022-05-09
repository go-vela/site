---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a pipeline.
---

## Endpoint

```
POST  /api/v1/pipelines/:org/:repo
```

## Parameters

The following parameters are used to configure the endpoint:

| Name       | Description          |
|------------|----------------------|
| `org`      | name of organization |
| `repo`     | name of repository   |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- |-----------------------------------------------------|
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
  "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
  "ref": "refs/heads/master",
  "type": "yaml",
  "version": "1",
  "steps": true,
  "data": "LS0tCnZlcnNpb246ICIxIgoKc3RlcHM6CiAgLSBuYW1lOiBlY2hvCiAgICBpbWFnZTogYWxwaW5lOmxhdGVzdAogICAgY29tbWFuZHM6IFtlY2hvIGZvb10="
}
```

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat"
```

#### Response

```json
{
  "id": 1,
  "repo_id": 1,
  "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
  "flavor": "",
  "platform": "",
  "ref": "refs/heads/master",
  "type": "yaml",
  "version": "1",
  "external_secrets": false,
  "internal_secrets": false,
  "services": false,
  "stages": false,
  "steps": true,
  "templates": false,
  "data": "LS0tCnZlcnNpb246ICIxIgoKc3RlcHM6CiAgLSBuYW1lOiBlY2hvCiAgICBpbWFnZTogYWxwaW5lOmxhdGVzdAogICAgY29tbWFuZHM6IFtlY2hvIGZvb10="
}
```
