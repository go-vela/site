---
title: "Type"
linkTitle: "Type"
description: >
  This section contains information on the type component for a template.
---

The `type` component is a part of a [template](/docs/concepts/pipeline/templates) for Vela.

This declaration allows you to provide the type of template provided from the remote system.

## Options

The following options are available to configure the component:

| Name     | Description                                                      |
| -------- | ---------------------------------------------------------------- |
| `github` | fetches the template from a GitHub or GitHub Enterprise instance |

#### GitHub

The `github` template type is designed to fetch templates from [GitHub](https://github.com) or [GitHub Enterprise](https://github.com/enterprise).

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

templates
  - name: template
    source: github.com/vela/atlas/cmd
+    type: github

steps:
  - name: test
    template:
      name: template
      vars:
        cmd: go test ./...

  - name: build
    template:
      name: template
      vars:
        cmd: go build
```

{{% alert color="info" %}}
This pipeline will execute the `test` step first, then run the `build` step.
{{% /alert %}}
