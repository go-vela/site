---
title: "Pull"
linkTitle: "Pull"
description: >
  This section contains information on the pull component for a step.
---

The `pull` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to control how and when Vela will attempt to pull the [image](/docs/concepts/pipeline/steps/image/) provided for the step.

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

steps:
  - name: test
    image: golang
+   pull: always
    commands:
      - go test ./...

  - name: build
    image: golang
+   pull: not_present
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
