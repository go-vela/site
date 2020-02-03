---
title: "Image"
linkTitle: "Image"
description: >
  This section contains information on the image component for a step.
---

The `image` component is a part of a [step](/docs/concepts/pipeline/steps) for Vela.

This declaration allows you to provide the [Docker image](https://docs.docker.com/engine/docker-overview/#images) used to create the ephemeral container.

{{% alert color="warning" %}}
All Vela steps will require an `image` declaration to be provided.
{{% /alert %}}

## Options

Any valid [Docker image](https://docs.docker.com/engine/docker-overview/#images) in any publicly accessible [Docker registry](https://docs.docker.com/registry/) can be used for the container.

```yaml
image: golang
image: golang:latest
image: golang:1.12
image: library/golang:1.12
image: index.docker.io/library/golang
image: index.docker.io/library/golang:1.12
```

{{% alert color="warning" %}}
All the above images would pull an image from the [golang Docker repository](https://hub.docker.com/_/golang).
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
+    image: golang
    commands:
      - go test ./...

  - name: build
+    image: golang
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
