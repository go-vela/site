---
title: "Multiline"
linkTitle: "Multiline"
description: >
  Example Go template with multiline strings.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a template.

If you're new to YAML we also recommend reviewing the [YAML 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

From [YAML Spec Scalars](https://yaml.org/spec/1.2/spec.html):

* `|` - In Scalar literals, newlines are preserved

```yaml
# Below YAML was taken from spec literal example
--- |
  \//||\/||
  // ||  ||__
```

{{% alert title="Tip:" color="info" %}}
For information on more types of scalars read the [spec information](https://yaml.org/spec/1.2/spec.html#id2760844)
{{% /alert %}}

## Sample

Let's take a look at using a conditional with a variable in a template:

```yaml
metadata:
  template: true

steps:

  {{ .test }}

  - name: build
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

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.yml
    type: github

steps:
  - name: golang
    template:  
      name: sample
      vars:
        test: |
          - name: test
              commands:
                - go test ./...
              image: golang:latest
              pull: always
              ruleset:
               event: [ push, pull_request ]
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
