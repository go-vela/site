---
title: "Secrets"
linkTitle: "Secrets"
description: >
  This section contains information on the secrets component for a pipeline.
---

The `secrets` component is a part of a [pipeline](/docs/concepts/pipeline/) for Vela.

This declaration allows you to provide sensitive information into the pipeline.

{{% alert color="info" %}}
A single, ephemeral run of a pipeline is known as a [build](/docs/concepts/system/build/).
{{% /alert %}}

Secrets are always retrieved at the beginning of a pipeline before any services, stages or steps are created or started. They are extremely useful when you don't want to provide sensitive information in plain text.

{{% alert color="info" %}}
Any variable provided with this declaration will allow step(s) to request access to these variables at runtime.
{{% /alert %}}

## Fields

The following fields are used to configure the component:

| Name     | Description                                  | Required |
| -------- | -------------------------------------------- | -------- |
| `engine` | name of storage backend to fetch secret from | `false`  |
| `key`    | path to secret to fetch from storage backend | `false`  |
| `name`   | name of secret to reference in the pipeline  | `true`   |
| `type`   | type of secret to fetch from storage backend | `false`  |

{{% alert color="info" %}}
The following fields have a default value already set:

- `engine`: `native`
- `key`: `<secret name>`
- `type`: `repo`
  {{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

+secrets:
+  - name: username
+    engine: native
+    key: username
+    type: repo
+  - name: password
+    engine: native
+    key: password
+    type: repo

steps:
  - name: test
    image: golang
    secrets: [ username, password ]
    commands:
      - echo "machine github.com" > .netrc
      - echo "login ${USERNAME}" >> .netrc
      - echo "password ${PASSWORD}" >> .netrc
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will allow the following secrets to be referenced:

- `username`
- `password`

This pipeline will also add the following environment variables to the `test` step:

- `USERNAME=<value>`
- `PASSWORD=<value>`
  {{% /alert %}}
