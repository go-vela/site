---
title: "Entrypoint"
linkTitle: "Entrypoint"
description: >
  This section contains information on the entrypoint component for a service.
---

The `entrypoint` component is a part of a [service](/docs/usage/concepts/pipeline/services) for Vela.

This declaration allows you to provide the command to execute inside the container.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
    image: postgres:12
+    entrypoint: "/docker-entrypoint.sh"

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
