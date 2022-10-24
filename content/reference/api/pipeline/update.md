---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a pipeline.
---

## Endpoint

```
PUT  /api/v1/pipelines/:org/:repo/:pipeline
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

#### File

```json
{
  "data": "LS0tCnZlcnNpb246ICIxIgoKc3RlcHM6CiAgLSBuYW1lOiBlY2hvCiAgICBpbWFnZTogYWxwaW5lOmxhdGVzdAogICAgZW52aXJvbm1lbnQ6CiAgICAgIEhFTExPOiB3b3JsZAogICAgY29tbWFuZHM6IFtlY2hvICRIRUxMT10="
}
```

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat/48afb5bdc41ad69bf22588491333f7cf71135163"
```

#### Response

```json
{
  "id": 1,
  "repo_id": 1,
  "commit": "48afb5bdc41ad69bf22588491333f7cf71135163",
  "flavor": "",
  "platform": "",
  "ref": "refs/heads/main",
  "type": "yaml",
  "version": "1",
  "external_secrets": false,
  "internal_secrets": false,
  "services": false,
  "stages": false,
  "steps": true,
  "templates": false,
  "data": "LS0tCnZlcnNpb246ICIxIgoKc3RlcHM6CiAgLSBuYW1lOiBlY2hvCiAgICBpbWFnZTogYWxwaW5lOmxhdGVzdAogICAgZW52aXJvbm1lbnQ6CiAgICAgIEhFTExPOiB3b3JsZAogICAgY29tbWFuZHM6IFtlY2hvICRIRUxMT10="
}
```
