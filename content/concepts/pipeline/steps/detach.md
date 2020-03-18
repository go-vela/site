---
title: "Detach"
linkTitle: "Detach"
description: >
  This section contains information on the detach component for a step.
---

The `detach` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to run the container in a detached (headless) state.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

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

  - name: run
    image: golang
+    detach: true
    commands:
      - ./main -http=:8080
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step and finally run the `run` step.
{{% /alert %}}
