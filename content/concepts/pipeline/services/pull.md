---
title: "Pull"
linkTitle: "Pull"
description: >
  This section contains information on the pull component for a service.
---

The `pull` component is a part of a [service](/docs/concepts/pipeline/services/) for Vela.

This declaration allows you to automatically upgrade to the latest version of the [image](/docs/concepts/pipeline/services/image/).

{{% alert color="info" %}}
Vela will always attempt to pull from its existing cache for images.

We recommend using the `pull` declaration whenever possible.
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
    image: postgres:12
+    pull: true

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
