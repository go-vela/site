---
title: "Multiline"
linkTitle: "Multiline"
description: >
  Learn how to write a Vela template that passes multiline strings.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a template.

If you're new to YAML we also recommend reviewing the [YAML 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

From [YAML Spec Scalars](https://yaml.org/spec/1.2/spec.html):

* `|` - In literals, newlines are preserved
> 
> ```yaml
> --- |
>   \//||\/||
>   // ||  ||__
> ```

* `>` - In the folded scalars, newlines become spaces

> ```yaml
> --- >
>   Mark McGwire's
>   year was crippled
>   by a knee injury.
> ```

{{% alert color="tip" %}}
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
    pull: true
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
      name: golang
      vars:
        test: |
          - name: test
              commands:
                - go test ./...
              image: golang:latest
              pull: true
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
    pull: true
    ruleset:
      event: [ push, pull_request ]

  - name: sample_build
    commands:
      - go build
    image: golang:latest
    pull: true
    ruleset:
      event: [ push, pull_request ]
```
