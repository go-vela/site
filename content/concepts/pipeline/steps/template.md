---
title: "Template"
linkTitle: "Template"
description: >
  This section contains information on the template component for a step.
---

The `template` component is a part of a [step](/docs/concepts/pipeline/steps) for Vela.

This declaration allows you to provide the name of template to expand in the pipeline.

## Fields

The following fields are used to configure the component:

| Name     | Description                                        | Required |
| -------- | -------------------------------------------------- | -------- |
| `name`   | unique identifier for the template in the pipeline | `true`   |
| `vars`   | variables injected into the template               | `false`  |

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

templates
  - name: template
    source: github.com/vela/atlas/cmd
    type: github

steps:
  - name: test
+    template:
+      name: template
+      vars:
+        cmd: go test ./...

  - name: build
+    template:
+      name: template
+      vars:
+        cmd: go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
