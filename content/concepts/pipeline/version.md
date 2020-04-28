---
title: "Version"
linkTitle: "Version"
description: >
  This section contains information on the version component for a pipeline.
---

The `version` component is a part of a [pipeline](/docs/concepts/pipeline/) for Vela.

This declaration allows you to provide the syntax version used to evaluate the pipeline.

{{% alert color="warning" %}}
All Vela pipelines will require a `version` declaration to be provided.
{{% /alert %}}

## Syntax

The following is an example of valid syntax for a `version` declaration:

```diff
+version: "1"

metadata:
  template: false

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
