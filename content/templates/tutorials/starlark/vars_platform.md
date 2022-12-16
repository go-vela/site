---
title: "Platform Vars"
linkTitle: "Platform Vars"
description: >
  Example Starlark template with platform vars.
---

{{% alert color="note" %}}
We recommend reviewing [Starlark Spec](https://github.com/bazelbuild/starlark/blob/master/spec.md) before attempting to create a template.

Additionally, depending on how the template is written, it may be incompatible with viewing pipelines in the UI.
{{% /alert %}}

## Overview

Platform variables can be referenced with the following syntax:

`ctx['vela']['<resource>']['<name>']`

## Examples

- `ctx["vela"]["repo"]["name"]` equates to the `VELA_REPO_NAME` environment variable
- `ctx["vela"]["build"]["number"]` equates to the `VELA_BUILD_NUMBER` environment variable
- `ctx["vela"]["system"]["addr"]` equates to the `VELA_ADDR` environment variable
- `ctx["vela"]["deployment"]["<name>"]` equates to the `DEPLOYMENT_PARAMETER_<name>` environment variable

## Sample

Let's take a look at using a platform variable within a template:

```python
def main(ctx):
  return {
    'version': '1',
    'steps': [
      step(ctx["vela"]["repo"]["name"]),
    ],
  }

def step(name):
  return {
    "name": "echo %s" % name,
    "image": "alpine:latest",
    'commands': [
      "echo %s" % name
    ]
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
```

Which means the compiled pipeline for execution on a worker is:

```yaml
version: 1
steps:
  - name: sample_echo hello-world
    image: alpine:latest
    commands:
      - echo hello-world
```
