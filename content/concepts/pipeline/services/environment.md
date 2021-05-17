---
title: "Environment"
linkTitle: "Environment"
description: >
  This section contains information on the environment component for a service.
---

The `environment` component is a part of a [service](/docs/concepts/pipeline/services/) for Vela.

This declaration allows you to provide variables injected into the container environment.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
    image: postgres:12
+    environment:
+      POSTGRES_DB: example
+      POSTGRES_USER: example

steps:
  - name: test
    image: golang
    environment:
      DATABASE_DRIVER: postgres
      DATABASE_CONFIG: 'postgres://example@postgres:5432/example?sslmode=disable'
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start the `postgres` service first, then run the `test` step.
{{% /alert %}}

## Defaults

{{% alert title="Tip:" color="info" %}}
Full list is available in the [environment reference](/docs/reference/environment/)
{{% /alert %}}