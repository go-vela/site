---
title: "Secrets"
linkTitle: "Secrets"
description: >
  This section contains information on the secrets component for a step.
---

The `secrets` component is a part of a [step](/docs/usage/concepts/pipeline/steps) for Vela.

This declaration allows you to provide sensitive variables injected into the container environment.

{{% alert color="info" %}}
Any variable provided with this declaration will be injected into the container as an upper case variable.
{{% /alert %}}

## Simple

The following is an example of valid syntax for the simple version of the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    secrets: [ git_username, git_password ]
    commands:
      - echo "machine github.com" > .netrc
      - echo "login ${GIT_USERNAME}" > .netrc
      - echo "password ${GIT_PASSWORD}" > .netrc
      - go test ./...

  - name: build
    image: golang
+    secrets: [ git_username, git_password ]
    commands:
      - echo "machine github.com" > .netrc
      - echo "login ${GIT_USERNAME}" > .netrc
      - echo "password ${GIT_PASSWORD}" > .netrc
      - go build
```

{{% alert color="info" %}}
This pipeline will add the following environment variables to the `test` and `build` steps:
* `GIT_USERNAME=<value>`
* `GIT_PASSWORD=<value>`

This pipeline will also execute the `test` step first, then run the `build` step.
{{% /alert %}}

## Advanced

#### Fields

The following fields are used to configure the advanced version of the component:

| Name     | Description                                 | Required |
| -------- | ------------------------------------------- | -------- |
| `source` | secret from pipeline to rename for step     | `true`   |
| `target` | target name for variable to inject for step | `true`   |

#### Syntax

The following is an example of valid syntax for the advanced version of the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    secrets:
+      - source: username
+        target: git_username
+      - source: password
+        target: git_password
    commands:
      - echo "machine github.com" > .netrc
      - echo "login ${GIT_USERNAME}" > .netrc
      - echo "password ${GIT_PASSWORD}" > .netrc
      - go test ./...

  - name: build
    image: golang
+    secrets:
+      - source: username
+        target: git_username
+      - source: password
+        target: git_password
    commands:
      - echo "machine github.com" > .netrc
      - echo "login ${GIT_USERNAME}" > .netrc
      - echo "password ${GIT_PASSWORD}" > .netrc
      - go build
```

{{% alert color="info" %}}
This pipeline will add the following environment variables to the `test` and `build` steps:
* `GIT_USERNAME=<value>`
* `GIT_PASSWORD=<value>`

This pipeline will also execute the `test` step first, then run the `build` step.
{{% /alert %}}
