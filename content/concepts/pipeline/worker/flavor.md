---
title: "Flavor"
linkTitle: "Flavor"
description: >
  This section contains information on the flavor component for a worker.
---

The `flavor` component is a part of a [template](/docs/concepts/pipeline/templates/) for Vela.

This declaration allows you to route your build to a single flavors within a Vela cluster.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

worker:
+  flavor: large

steps:
  - name: test
    image: golang
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start and run on a worker with the available route `large`
{{% /alert %}}
