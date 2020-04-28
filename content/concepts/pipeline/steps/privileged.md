---
title: "Privileged"
linkTitle: "Privileged"
description: >
  This section contains information on the privileged component for a step.
---

The `privileged` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to run the container with extra privileges.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    privileged: true
    commands:
      - go test ./...

  - name: build
    image: golang
+    privileged: true
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
