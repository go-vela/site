---
title: "Platform Vars"
linkTitle: "Platform Vars"
description: >
  Example Go template with platform vars.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a template.

If you're new to YAML we also recommend reviewing the [YAML 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

Platform variables can be referenced with the following syntax:

`{{ vela "<environment variable>" }}`

## Examples

- `{{ vela "VELA_FULL_REPO_NAME" }}` equates to the `VELA_FULL_REPO_NAME` environment variable
- `{{ vela "FULL_REPO_NAME" }}` equates to the `VELA_REPO_NAME` environment variable
- `{{ vela "VELA_BUILD_NUMBER" }}` equates to the `VELA_BUILD_NUMBER` environment variable
- `{{ vela "VELA_ADDR" }}` equates to the `VELA_ADDR` environment variable

## Sample

Let's take a look at using a platform variable in a template:

```yaml
metadata:
  template: true

steps:
  - name: test
    commands:
      - echo {{ vela "VELA_REPO_FULL_NAME" }}
    image: alpine
    pull: always
    ruleset:
      event: [ push, pull_request ]
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.yml
    type: github

steps:
  - name: sample
    template:
      name: echo
```

Which means the compiled pipeline for execution on a worker is:

```yaml
version: "1"
steps:
  - name: sample_echo
    commands:
      - echo github/octocat
    image: alpine
    pull: always
    ruleset:
      event: [ push, pull_request ]
```
