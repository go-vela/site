---
title: 'Environment'
linkTitle: 'Environment'
description: >
  This section contains information on the environment component for a step.
---

The `environment` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to provide variables injected into the container environment.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    environment:
+      CGO_ENABLED: '0'
+      GOOS: linux
+      GOARCH: amd64
    commands:
      - go test ./...

  - name: build
    image: golang
+    environment:
+      CGO_ENABLED: '0'
+      GOOS: linux
+      GOARCH: amd64
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}

## Defaults

{{% alert title="Tip:" color="info" %}}
Full list is available in the [environment reference](/docs/reference/environment/)
{{% /alert %}}
