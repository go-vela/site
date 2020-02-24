---
title: "Entrypoint"
linkTitle: "Entrypoint"
description: >
  This section contains information on the entrypoint component for a step.
---

The `entrypoint` component is a part of a [step](/docs/concepts/pipeline/steps) for Vela.

This declaration allows you to provide the command to execute inside the container.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
   template: false

steps:
  - name: test
    image: golang
+    entrypoint: /usr/local/go/bin/go
    commands:
      - go test ./...

  - name: build
    image: golang
+    entrypoint: /usr/local/go/bin/go
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
