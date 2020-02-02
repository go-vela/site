---
title: "Commands"
linkTitle: "Commands"
description: >
  This section contains information on the commands component for a step.
---

The `commands` component is a part of a [step](/docs/usage/concepts/pipeline/steps) for Vela.

This declaration allows you to provide execution instructions to run inside the container.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    commands:
+      - go test ./...

  - name: build
    image: golang
+    commands:
+      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
