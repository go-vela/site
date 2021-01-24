---
title: "Conditionals"
linkTitle: "Conditionals"
description: >
  Example Starlark template with conditionals.
---

{{% alert color="note" %}}
We recommend reviewing [Starlark Spec](https://github.com/bazelbuild/starlark/blob/master/spec.md) before attempting to create a template.
{{% /alert %}}

## Overview

From [Starlark Conditional Expressions](https://github.com/google/starlark-go/blob/master/doc/spec.md#conditional-expressions):

```text
"yes" if enabled else "no"
```

{{% alert color="tip" %}}
For information on if/else statements see [conditional docs](https://github.com/google/starlark-go/blob/master/doc/spec.md#conditional-expressions)
{{% /alert %}}

## Sample

Let's take a look at using a conditional with a variable in a template:

```python
def main(ctx):
  steps = [
              {
                  "name": "test",
                  "image": ctx["vars"]["image"],
                  "commands": [
                      "go test ./..."
                  ],
                  "pull": ctx["vars"]["pull_policy"],
                  "ruleset": {
                      "event": [
                          "push",
                          "pull_request"
                      ]
                  }
              }
          ]

  # if branch equals master add this step to the final pipeline
  if ctx["vela"]["build"]["branch"] == "master":
      steps.append(
          {
              "name": "build",
              "image": ctx["vars"]["image"],
              "commands": [
                  "go build"
              ],
              "pull": ctx["vars"]["pull_policy"],
              "ruleset": {
                  "event": [
                      "push",
                      "pull_request"
                  ]
              }
          }
      )

  return {
      'version': '1',
      'steps': steps,
  }
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.star
    type: github
    format: starlark

steps:
  - name: sample
    template:
      name: golang
      vars:
        image: golang:latest
        pull_policy: "always"
```

Which means the compiled pipeline for execution on a worker is:

```yaml
version: "1"
steps:
  - name: sample_test
    commands:
      - go test ./...
    image: golang:latest
    pull: always
    ruleset:
      event: [ push, pull_request ]

  - name: sample_build
    commands:
      - go build
    image: golang:latest
    pull: always
    ruleset:
      event: [ push, pull_request ]
```
