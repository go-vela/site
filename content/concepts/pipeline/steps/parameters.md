---
title: "Parameters"
linkTitle: "Parameters"
description: >
  This section contains information on the parameters component for a step.
---

The `parameters` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to provide extra configuration variables for a plugin.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: plugin
    image: target/vela-docker:v0.1.0
    pull: always
+    parameters:
+      registry: index.docker.io
+      repo: index.docker.io/octocat/hello-world
```

{{% alert color="info" %}}
This pipeline will add the following environment variables to the `plugin` step:

- `PARAMETER_REGISTRY=index.docker.io`
- `PARAMETER_REPO=index.docker.io/octocat/hello-world`
  {{% /alert %}}
