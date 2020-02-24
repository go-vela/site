---
title: "Ports"
linkTitle: "Ports"
description: >
  This section contains information on the ports component for a service.
---

The `ports` component is a part of a [service](/docs/concepts/pipeline/services) for Vela.

This declaration allows you to provide a list of ports to map for the container in the pipeline.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
    image: postgres:12
+    ports:
+      - "5432:5432"

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
