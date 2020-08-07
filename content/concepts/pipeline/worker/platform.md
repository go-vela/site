---
title: "Platform"
linkTitle: "Platform"
description: >
  This section contains information on the platform component for a worker.
---

The `platform` component is a part of a [template](/docs/concepts/pipeline/templates/) for Vela.

This declaration allows you to route your build to a single platform within a Vela cluster.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

worker:
+  platform: docker

steps:
  - name: test
    image: golang
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start and run on a worker with the available route `docker`
{{% /alert %}}