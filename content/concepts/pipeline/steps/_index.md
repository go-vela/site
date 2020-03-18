---
title: "Steps"
linkTitle: "Steps"
description: >
  This section contains information on the steps component for a pipeline.
---

The `steps` component is a part of a [pipeline](/docs/concepts/pipeline/) for Vela.

This declaration allows you to provide sequential, execution instructions for a pipeline.

{{% alert color="info" %}}
A single, ephemeral run of a pipeline is known as a [build](/docs/concepts/system/build/).
{{% /alert %}}

Steps are always executed, in the order they are defined, inside an ephemeral [Docker container](https://www.docker.com/resources/what-container).

If the container returns a non-zero exit code, the build immediately terminates and returns a failure status.

{{% alert color="info" %}}
To run `steps` in parallel, you can visit the [stages documentation](/docs/concepts/pipeline/stages/).
{{% /alert %}}

## Fields

The following fields are used to configure the component:

| Name          | Description                                                 | Required |
| ------------- | ----------------------------------------------------------- | -------- |
| `commands`    | execution instructions to run inside the container          | `false`  |
| `detach`      | enables running the container in a headless mode            | `false`  |
| `entrypoint`  | command to execute inside the container                     | `false`  |
| `environment` | variables injected into the container environment           | `false`  |
| `image`       | Docker image used to create ephemeral container             | `true`   |
| `name`        | unique identifier for the container in the pipeline         | `true`   |
| `parameters`  | extra configuration variables for a plugin                  | `false`  |
| `privileged`  | enables running the container with extra privileges         | `false`  |
| `pull`        | enable pulling the latest version of the image              | `false`  |
| `ruleset`     | conditions to limit the execution of the container          | `false`  |
| `secrets`     | sensitive variables injected into the container environment | `false`  |
| `template`    | name of template to expand in the pipeline                  | `false`  |

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

+steps:
+  - name: test
+    image: golang
+    commands:
+      - go test ./...
+
+  - name: build
+    image: golang
+    commands:
+      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
