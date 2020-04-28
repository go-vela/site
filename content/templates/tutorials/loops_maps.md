---
title: "Loops with Maps"
linkTitle: "Loops with Maps"
description: >
  Learn how to write a Vela template with loops and maps.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a templates.

 If you're new to Yaml we also recommend reviewing the [Yaml 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

From [Go template range](https://golang.org/pkg/text/template/#hdr-Actions):

```text
{{range pipeline}}
  T1 
{{end}}
```

> The value of the pipeline must be an array, slice, map, or channel.
> If the value of the pipeline has length zero, nothing is output;
> otherwise, dot is set to the successive elements of the array,
> slice, or map and T1 is executed. If the value is a map and the
> keys are of basic type with a defined order, the elements will be
> visited in sorted key order.

{{% alert color="tip" %}}
For information on range/else statements see [conditional docs](https://golang.org/pkg/text/template/#hdr-Actions)
{{% /alert %}}

## Sample

Lets take a look at ranging over a map for a template:

```yaml
metadata:
  template: true

steps:

  {{ range $key, $value := .images }}

  - name: test{{ $key }}
    commands:
      - go test ./...
    image: {{ $value }}
    {{ .pull_policy }}
    ruleset:
      event: [ push, pull_request ]

  {{ end }}

  - name: build
    commands:
      - go build
    environment:
      CGO_ENABLED: '0'
      GOOS: linux
    image: golang:latest
    {{ .pull_policy }}
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
        pull_policy: "pull: true"
        images:
          _latest: golang:latest
          _1.13: golang:1.13
          _1.12: golang:1.13
```

Which means the compiled pipeline for execution on a worker is:

{{% alert color="warning" %}}
Go does not guarantee order with maps. If you need the steps to **always** be outputted in the same order use the loops with slice implementation.
{{% /alert %}}

```yaml
version: "1"
steps:
  - name: sample_test_latest
    commands:
      - go test ./...
    image: golang:latest
    pull: true
    ruleset:
      event: [ push, pull_request ]

  - name: sample_test_1.13
    commands:
      - go test ./...
    image: golang:1.13
    pull: true
    ruleset:
      event: [ push, pull_request ]

  - name: sample_test_1.12
    commands:
      - go test ./...
    image: golang:1.12
    pull: true
    ruleset:
      event: [ push, pull_request ]

  - name: sample_build
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
