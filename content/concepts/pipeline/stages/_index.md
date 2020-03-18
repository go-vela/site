---
title: "Stages"
linkTitle: "Stages"
description: >
  This section contains information on the stages component for a pipeline.
---

The `stages` component is a part of a [pipeline](/docs/concepts/pipeline/) for Vela.

This declaration allows you to provide parallel, execution instructions for a pipeline.

{{% alert color="info" %}}
A single, ephemeral run of a pipeline is known as a [build](/docs/concepts/system/build/).
{{% /alert %}}

Stages are always executed, in parallel, and are comprised of one or many [steps](/docs/concepts/pipeline/steps/).

## Fields

The following fields are used to configure the component:

| Name    | Description                                               | Required |
| ------- | --------------------------------------------------------- | -------- |
| `name`  | unique identifier for the stage in the pipeline           | `false`  |
| `needs` | stages that must complete before starting the current one | `false`  |
| `steps` | sequential execution instructions for the stage           | `true`   |

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

+stages:
+  test:
+    steps:
+      - name: test
+        image: golang
+        commands:
+          - go test ./...
+  build:
+    steps:
+      - name: build
+        image: golang
+        commands:
+          - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` stage and the `build` stage at the same time.
{{% /alert %}}
