---
title: "Image"
linkTitle: "Image"
description: >
  This section contains information on the image component for a service.
---

The `image` component is a part of a [service](/docs/usage/concepts/pipeline/services) for Vela.

This declaration allows you to provide the [Docker image](https://docs.docker.com/engine/docker-overview/#images) used to create the ephemeral container.

{{% alert color="warning" %}}
All Vela services will require an `image` declaration to be provided.
{{% /alert %}}

## Examples

Any valid [Docker image](https://docs.docker.com/engine/docker-overview/#images) in any publicly accessible [Docker registry](https://docs.docker.com/registry/) can be used for the container.

```yaml
image: golang
image: golang:latest
image: golang:1.12
image: library/golang:1.12
image: index.docker.io/library/golang
image: index.docker.io/library/golang:1.12
```

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
+    image: postgres:12
    pull: true

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
