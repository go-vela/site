---
title: "Environment"
weight: 3
description: >
  Set environment variables for your step.
---

The environment declaration for a build step instructs Vela to insert the given input as environment variables.

{{% alert title="Warning" color="warning" %}}
You should not use environment for plugin parameters or secrets.

Please see [parameters](../parameters/) or [secrets](../secrets/).
{{% /alert %}}

```diff
steps:
  - name: install
    image: golang:latest
    pull: true
+   environment:
+     CGO_ENABLED: '0'
+     GOOS: linux
    commands:
      - go get ./...
```
