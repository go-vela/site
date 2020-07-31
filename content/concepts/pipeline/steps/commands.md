---
title: "Commands"
linkTitle: "Commands"
description: >
  This section contains information on the commands component for a step.
---

The `commands` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to provide execution instructions to run inside the container.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: build
    image: golang
+   commands:
+     - go test ./...
+     - go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}

Using the above example, the provided commands are converted to a simple shell script that looks like:

```sh
#!/bin/sh

set -e

go test ./...

go build
```

In turn, the above shell script is executed as the Docker entrypoint for the container:

```sh
docker run --entrypoint=build.sh golang
```