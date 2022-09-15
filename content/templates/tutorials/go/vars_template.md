---
title: "Template Vars"
linkTitle: "Template Vars"
description: >
  Example Golang template with template vars.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a template.

If you're new to YAML we also recommend reviewing the [YAML 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

Template variables can be referenced with the following syntax:

`{{ .name }}`

## Sample

Let's take a look at using variables within a template:

```yaml
metadata:
  template: true

steps:
  - name: test
    commands:
      - echo {{ .input }}
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
      vars:
        input: hello
```

Which means the compiled pipeline for execution on a worker is:

```yaml
version: "1"
steps:
  - name: sample_echo
    commands:
      - echo hello
    image: alpine
    pull: always
    ruleset:
      event: [ push, pull_request ]
```
