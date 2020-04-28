---
title: "Source"
linkTitle: "Source"
description: >
  This section contains information on the source component for a template.
---

The `source` component is a part of a [template](/docs/concepts/pipeline/templates/) for Vela.

This declaration allows you to provide the path to the template in the remote system.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

templates
  - name: template
+    source: github.com/vela/atlas/cmd
    type: github

steps:
  - name: test
    template:
      name: template
      vars:
        cmd: go test ./...

  - name: build
    template:
      name: template
      vars:
        cmd: go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
