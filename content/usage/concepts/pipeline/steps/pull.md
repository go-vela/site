---
title: "Pull"
linkTitle: "Pull"
description: >
  This section contains information on the pull component for a step.
---

The `pull` component is a part of a [step](/docs/usage/concepts/pipeline/steps) for Vela.

This declaration allows you to automatically upgrade to the latest version of the [image](/docs/usage/concepts/pipeline/step/image).

{{% alert color="info" %}}
Vela will always attempt to pull from its existing cache for images.

We recommend using the `pull` declaration whenever possible.
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    pull: true
    commands:
      - go test ./...

  - name: build
    image: golang
+    pull: true
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
