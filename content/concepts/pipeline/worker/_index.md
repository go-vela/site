---
title: "Worker"
linkTitle: "Worker"
description: >
  This section contains information on the worker component for a pipeline.
---

The `worker` component is a part of a [pipeline](/docs/concepts/pipeline/) for Vela.

This declaration allows you to route your build to a subset of workers within a Vela cluster.

{{% alert color="info" %}}
Routes can **only** be made by a system administrator. 
{{% /alert %}}

Routing can guarantee a build is ran on a specific platform or runtime within a cluster. This may be extremely useful when your building artifacts that can only be built on specific architectures.

{{% alert color="warning" %}}
It's import to remember that pinning yourself to workers lowers the number of available workers you can run on. 
{{% /alert %}}

## Fields

The following fields are used to configure the component:

| Name       | Description                                                     | Required |
| ---------- | --------------------------------------------------------------- | -------- |
| `platform` | run a build on a specific platform available within the cluster | `false`  |
| `flavor`   | run a build on a flavor of workers within platform              | `false`  |

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

+worker:
+  platform: docker
+  flavor: large

steps:
  - name: test
    image: golang
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start and run on a worker with the available route `docker:large`
{{% /alert %}}
