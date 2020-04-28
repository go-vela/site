---
title: "Needs"
linkTitle: "Needs"
description: >
  This section contains information on the needs component for a stage.
---

The `needs` component is a part of a [stage](/docs/concepts/pipeline/stages/) for Vela.

This declaration allows you to provide other stages that must complete before starting the current one.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

stages:
  test:
    steps:
      - name: test
        image: golang
        commands:
          - go test ./...
  build:
+    needs: [ test ]
    steps:
      - name: build
        image: golang
        commands:
          - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` stage first, then run the `build` stage.
{{% /alert %}}
