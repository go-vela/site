---
title: "Template Vars"
linkTitle: "Template Vars"
description: >
  Example Starlark template with template vars.
---

{{% alert color="note" %}}
We recommend reviewing [Starlark Spec](https://github.com/bazelbuild/starlark/blob/master/spec.md) before attempting to create a template.
{{% /alert %}}

## Overview

Template variables can be referenced with the following syntax:

`ctx['vars'][<name>]`

## Sample

Let's take a look at using variables within a template:

```python
def main(ctx):
    steps = [step(x, ctx["vars"]["pull_policy"], ctx["vars"]["commands"]) for x in ctx["vars"]["tags"]]

    pipeline = {
        'version': '1',
        'steps': steps,
    }

    return pipeline

def step(tag, pull_policy, commands):
    return {
        "name": "build %s" % tag,
        "image": "golang:%s" % tag,
        "pull": pull_policy,
        'commands': commands.values(),
    }
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.star
    format: starlark
    type: github

steps:
  - name: build
    template:
      name: sample
      vars:
        tags: [latest, "1.14", "1.15"]
        pull_policy: always
        commands:
          test: "go test ./..."
          build: "go build"
```

Which means the compiled pipeline for execution on a worker is:

```yaml
version: 1
steps:
  - name: sample_build latest
    image: golang:latest
    pull: always
    commands:
      - go test ./...
      - go build

  - name: sample_build 1.14
    image: golang:1.14
    pull: always
    commands:
      - go test ./...
      - go build

  - name: sample_build 1.15
    image: golang:1.15
    pull: always
    commands:
      - go test ./...
      - go build
```
