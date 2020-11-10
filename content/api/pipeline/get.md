---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to get a pipeline configuration.
---

## Endpoint

```
GET  /api/v1/pipelines/:org/:repo
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |
| `ref`   | file ref for fetching from the source provider   |
| `output`   | format the output for the pipeline configuration    |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | unable to retrieve the pipeline configuration |
| `401`       | indicates the user does not have proper permissions |
| `404`       | unable to retrieve the pipeline configuration |
| `500`       | system error while retrieving the pipeline configuration |

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
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat"
```

#### Response

```json
{
  "version": "1",
  "metadata": {},
  "worker": {},
  "steps": [
    {
      "ruleset": {
        "if": {
          "event": [
            "push"
          ]
        },
        "unless": {},
        "matcher": "filepath",
        "operator": "and"
      },
      "commands": [
        "echo \"hello\""
      ],
      "template": {},
      "image": "golang",
      "name": "hello",
      "pull": "not_present"
    }
  ]
}
```

```yaml
version: "1"
steps:
  - name: hello
    image: golang
    ruleset:
      event: push
    commands:
      - echo "hello"
```