---
title: "Metadata"
linkTitle: "Metadata"
description: >
  This section contains information on the metadata component for a pipeline.
---

The `metadata` component is a part of a [pipeline](/docs/usage/concepts/pipeline) for Vela.

This declaration allows extra information to be passed to the pipeline.

## Fields

The following fields are used to configure the component:

| Name       | Description                                  | Required |
| ---------- | -------------------------------------------- | -------- |
| `template` | enables compiling the pipeline as a template | `false`  |

## Syntax

The following is an example of valid syntax for a `metadata` declaration:

```diff
version: "1"

+metadata:
+  template: false

steps:
  - name: test
    image: golang
    commands:
      - go test ./...

  - name: build
    image: golang
    commands:
      - go build
```
