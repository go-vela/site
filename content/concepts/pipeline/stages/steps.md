---
title: "Steps"
linkTitle: "Steps"
description: >
  This section contains information on the steps component for a stage.
---

The `steps` component is a part of a [stage](/docs/concepts/pipeline/stages/) for Vela.

This declaration allows you to provide sequential, execution instructions for a stage.

{{% alert color="info" %}}
For more information, you can visit the [steps documentation](/docs/concepts/pipeline/steps/).
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

stages:
  test:
+    steps:
+      - name: test
+        image: golang
+        commands:
+          - go test ./...
  build:
+    steps:
+      - name: build
+        image: golang
+        commands:
+          - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` stage and the `build` stage at the same time.
{{% /alert %}}
