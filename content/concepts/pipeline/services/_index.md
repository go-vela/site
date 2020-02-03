---
title: "Steps"
linkTitle: "Steps"
description: >
  This section contains information on the services component for a pipeline.
---

The `services` component is a part of a [pipeline](/docs/usage/concepts/pipeline) for Vela.

This declaration allows you to provide detached (headless), execution instructions for a pipeline.

{{% alert color="info" %}}
A single, ephemeral run of a pipeline is known as a [build](/docs/usage/concepts/resources/build).
{{% /alert %}}

Services are always executed, in parallel inside an ephemeral [Docker container](https://www.docker.com/resources/what-container). They are extremely useful when your testing requires additional services such as a cache, database or queue.

{{% alert color="info" %}}
Services are always created at the beginning of a pipeline.
{{% /alert %}}

## Fields

The following fields are used to configure the component:

| Name          | Description                                                 | Required |
| ------------- | ----------------------------------------------------------- | -------- |
| `entrypoint`  | command to execute inside the container                     | `false`  |
| `environment` | variables injected into the container environment           | `false`  |
| `image`       | Docker image used to create ephemeral container             | `true`   |
| `name`        | unique identifier for the container in the pipeline         | `true`   |
| `ports`       | list of ports to map for the container in the pipeline      | `false`  |
| `pull`        | enable pulling the latest version of the image              | `false`  |

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

+services:
+  - name: postgres
+    image: postgres:12

steps:
  - name: test
    image: golang
    environment:
      DATABASE_DRIVER: postgres
      DATABASE_CONFIG: 'postgres://postgres@postgres:5432/postgres?sslmode=disable'
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start the `postgres` service first, then run the `test` step.
{{% /alert %}}
