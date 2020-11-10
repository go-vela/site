---
title: "Templates"
linkTitle: "Templates"
description: >
  Learn how to list pipeline templates.
---

## Endpoint

```
GET  /api/v1/pipelines/:org/:repo/templates
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |
| `ref`   | file ref for fetching from the source provider   |
| `output`   | format the output for the pipeline templates    |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | unable to retrieve the pipeline configuration templates |
| `401`       | indicates the user does not have proper permissions |
| `404`       | unable to retrieve the pipeline configuration or templates |
| `500`       | system error while retrieving the pipeline configuration templates |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat/templates"
```

#### Response

```json
{
  "some_template": {
    "link": "https://github.com/github/octocat/blob/master/template.yml",
    "name": "some_template",
    "source": "github.com/github/octocat/template.yml",
    "type": "github"
  },
}
```

```yaml
some_template:
  link: https://github.com/github/octocat/blob/master/template.yml
  name: some_template
  source: github.com/github/octocat/template.yml
  type: github
```