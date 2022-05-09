---
title: "Compile"
linkTitle: "Compile"
description: >
  Learn how to compile a pipeline configuration with templates.
---

## Endpoint

```
POST  /api/v1/pipelines/:org/:repo/:pipeline/compile
```

## Parameters

The following parameters are used to configure the endpoint:

| Name       | Description                                               |
|------------|-----------------------------------------------------------|
| `org`      | name of organization                                      |
| `repo`     | name of repository                                        |
| `pipeline` | commit SHA for pipeline from repository                   |
| `output`   | format the output for the compiled pipeline configuration |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | unable to retrieve or compile the pipeline configuration and templates |
| `401`       | indicates the user does not have proper permissions |
| `404`       | unable to retrieve or compile the pipeline configuration or templates |
| `500`       | system error while retrieving or compiling the pipeline configuration templates |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X POST \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/pipelines/github/octocat/48afb5bdc41ad69bf22588491333f7cf71135163/compile"
```

#### Response

{{% alert color="warning" %}}
Notice, when compiling a pipeline configuration step fields such as `image` and `commands` will be arranged in alphabetical order.
{{% /alert %}}

```yaml
version: "1"
secrets:
- name: go_module
  key: github/octocat/template_secret
  engine: native
  type: repo
steps:
- commands:
  - go vet ./... && git diff --exit-code; code=$?; git checkout -- .; (exit $code)
  - go fmt ./... && git diff --exit-code; code=$?; git checkout -- .; (exit $code)
  image: golang:latest
  name: go_validate
  pull: not_present
- commands:
  - go test ./...
  image: golang:latest
  name: go_test
  pull: not_present
- commands:
  - go build -a -ldflags '-extldflags "-static"' -o release/heyvela {$GO_MODULE}
  image: golang:latest
  name: go_build
  pull: not_present
  environment:
    CGO_ENABLED: "0"
    GOOS: linux
templates:
- name: go
  source: github.com/github/octocat/go/template.yml
  type: github
```

```json
{
  "version": "1",
  "metadata": {},
  "worker": {},
  "secrets": [
    {
      "name": "go_module",
      "key": "github/octocat/template_secret",
      "engine": "native",
      "type": "repo",
      "origin": {
        "ruleset": {
          "if": {},
          "unless": {}
        }
      }
    }
  ],
  "steps": [
    {
      "ruleset": {
        "if": {},
        "unless": {}
      },
      "commands": [
        "go vet ./... && git diff --exit-code; code=$?; git checkout -- .; (exit $code)",
        "go fmt ./... && git diff --exit-code; code=$?; git checkout -- .; (exit $code)"
      ],
      "template": {},
      "image": "golang:latest",
      "name": "go_validate",
      "pull": "not_present"
    },
    {
      "ruleset": {
        "if": {},
        "unless": {}
      },
      "commands": [
        "go test ./..."
      ],
      "template": {},
      "image": "golang:latest",
      "name": "go_test",
      "pull": "not_present"
    },
    {
      "ruleset": {
        "if": {},
        "unless": {}
      },
      "commands": [
        "go build -a -ldflags '-extldflags \"-static\"' -o release/heyvela {$GO_MODULE}"
      ],
      "template": {},
      "image": "golang:latest",
      "name": "go_build",
      "pull": "not_present",
      "environment": {
        "CGO_ENABLED": "0",
        "GOOS": "linux"
      }
    },
    {
      "ruleset": {
        "if": {},
        "unless": {}
      },
      "commands": [
        "go vet ./... && git diff --exit-code; code=$?; git checkout -- .; (exit $code)",
        "go fmt ./... && git diff --exit-code; code=$?; git checkout -- .; (exit $code)"
      ],
      "template": {},
      "image": "golang:latest",
      "name": "go-tag_validate",
      "pull": "not_present"
    },
    {
      "ruleset": {
        "if": {},
        "unless": {}
      },
      "commands": [
        "go test ./..."
      ],
      "template": {},
      "image": "golang:latest",
      "name": "go-tag_test",
      "pull": "not_present"
    },
    {
      "ruleset": {
        "if": {},
        "unless": {}
      },
      "commands": [
        "go build -a -ldflags '-extldflags \"-static\"' -o release/heyvela {$GO_MODULE}"
      ],
      "template": {},
      "image": "golang:latest",
      "name": "go-tag_build",
      "pull": "not_present",
      "environment": {
        "CGO_ENABLED": "0",
        "GOOS": "linux"
      }
    },
  ],
  "templates": [
    {
      "name": "go",
      "source": "github.com/github/octocat/go/template.yml",
      "type": "github"
    }
  ]
}
```