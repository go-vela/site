---
title: "Pull"
linkTitle: "Pull"
description: >
  This section contains information on the pull component for a service.
---

The `pull` component is a part of a [service](/docs/concepts/pipeline/services/) for Vela.

This declaration allows you to control how and when Vela will attempt to pull the [image](/docs/concepts/pipeline/services/image/) provided for the service.

{{% alert color="info" %}}
This component has a default value of `not_present`.

This means Vela will always attempt to pull from its existing cache for images.
{{% /alert %}}

## Options

The following options are available to configure the component:

| Name          | Description                                                       |
| ------------- | ----------------------------------------------------------------- |
| `always`      | attempt to pull the image even if it exists in the local cache    |
| `never`       | assumes the image already exists in the local cache               |
| `not_present` | only pull the image if it does not exist in the local cache       |
| `on_start`    | waits to pull the image until right before starting the container |

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
    image: postgres:12
+   pull: not_present

steps:
  - name: test
    image: golang
+   pull: always
    environment:
      DATABASE_DRIVER: postgres
      DATABASE_CONFIG: 'postgres://postgres@postgres:5432/postgres?sslmode=disable'
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start the `postgres` service first, then run the `test` step.
{{% /alert %}}
