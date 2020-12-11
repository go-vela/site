---
title: "Conditionals"
linkTitle: "Conditionals"
description: >
  Learn how to write a Vela template with conditionals.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a template.

If you're new to YAML we also recommend reviewing the [YAML 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

From [Go template Conditional](https://golang.org/pkg/text/template/#hdr-Actions):

```text
{{if pipeline}}
  T1
{{end}}
```

> If the value of the pipeline is empty, no output is generated;
> otherwise, T1 is executed. The empty values are false, 0, any
> nil pointer or interface value, and any array, slice, map, or
> string of length zero.
> Dot is unaffected.

{{% alert color="tip" %}}
For information on if/else statements see [conditional docs](https://golang.org/pkg/text/template/#hdr-Actions)
{{% /alert %}}

## Sample

Let's take a look at using a conditional with a variable in a template:

```yaml
metadata:
  template: true

{{$br := .branch}}

steps:

  - name: test
    commands:
      - go test ./...
    image: {{ .image }}
    {{ .pull_policy }}
    ruleset:
      event: [ push, pull_request ]

  # if branch equals master add this step to the final pipeline
  {{ if (eq $br "master") }}

  - name: build
    commands:
      - go build
    image: {{ .image }}
    {{ .pull_policy }}
    ruleset:
      event: [ push, pull_request ]

  {{ end }}
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
        image: golang:latest
        pull_policy: "pull: always"
        branch: master
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
