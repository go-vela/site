---
title: "Loops with Maps"
linkTitle: "Loops with Maps"
description: >
  Example Starlark template with loops and maps.
---

{{% alert color="note" %}}
We recommend reviewing [Starlark Spec](https://github.com/bazelbuild/starlark/blob/master/spec.md) before attempting to create a template.
{{% /alert %}}

## Overview

From [Starlark for loops](https://github.com/google/starlark-go/blob/master/doc/spec.md#for-loops):

```python
for i in [["a", 1], ["b", 2], ["c", 3]]:
  print(a, i) # prints "a 1", "b 2", "c 3"
```

## Sample

Let's take a look at looping over a map for a template:

```python
def main(ctx):
  ruleset = {
    "event": [
      "push",
      "pull_request"
    ]
  }

  steps = [
    {
      "name": "install",
      "image": "golang:latest",
      "commands": [
          "go get ./..."
      ],
      "pull": ctx["vars"]["pull_policy"],
      "ruleset": ruleset,
    }
  ]

  for name, image in ctx["vars"]["images"].items():
    steps.append(
        {
          "name": "test_%s" % name,
          "image": image,
          "commands": [
              "go test ./..."
          ],
          "pull": ctx["vars"]["pull_policy"],
          "ruleset": ruleset,
        }
    )

  steps.append(
    {
      "name": "build",
      "image": "golang:latest",
      "commands": [
          "go build"
      ],
      "environment": {
          "CGO_ENABLED": "0",
          "GOOS": "linux",
      },
      "pull": ctx["vars"]["pull_policy"],
      "ruleset": ruleset,
    }
  )

  pipeline = {
    'version': '1',
    'steps': steps,
  }

  return pipeline
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.star
    type: github

steps:
  - name: sample
    template:
      name: golang
      vars:
        pull_policy: "always"
        images:
          _latest: golang:latest
          _1.13: golang:1.13
          _1.12: golang:1.12
```

Which means the compiled pipeline for execution on a worker is:

{{% alert color="warning" %}}
Vela does not guarantee order with maps. If you need the steps to **always** be outputted in the same order use the loops with slice implementation.
{{% /alert %}}

```yaml
version: "1"
steps:
  - name: sample_test_latest
    commands:
      - go test ./...
    image: golang:latest
    pull: always
    ruleset:
      event: [ push, pull_request ]

  - name: sample_test_1.13
    commands:
      - go test ./...
    image: golang:1.13
    pull: always
    ruleset:
      event: [ push, pull_request ]

  - name: sample_test_1.12
    commands:
      - go test ./...
    image: golang:1.12
    pull: always
    ruleset:
      event: [ push, pull_request ]

  - name: sample_build
    commands:
      - go build
    environment:
      CGO_ENABLED: '0'
      GOOS: linux
    image: golang:latest
    pull: always
    ruleset:
      event: [ push, pull_request ]
```
