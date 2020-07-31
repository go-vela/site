---
title: "Ruleset"
linkTitle: "Ruleset"
description: >
  This section contains information on the ruleset component for a step.
---

The `ruleset` component is a part of a [step](/docs/concepts/pipeline/steps/) for Vela.

This declaration allows you to provide conditions to limit the execution of the container.

## Simple

#### Fields

The following fields are used to configure the simple version of the component:

| Name     | Description                         | Required |
| -------- | ----------------------------------- | -------- |
| `branch` | name of branch for build            | `false`  |
| `event`  | name of event for build             | `false`  |
| `path`   | path to workspace files for build   | `false`  |
| `repo`   | name of repo for build              | `false`  |
| `status` | name of status for build            | `false`  |
| `tag`    | name of reference for build         | `false`  |
| `target` | name of deployment target for build | `false`  |

#### Syntax

The following is an example of valid syntax for the simple version of the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    ruleset:
+      branch: master
+      event: push
    commands:
      - go test ./...

  - name: build
    image: golang
+    ruleset:
+      branch: master
+      event: push
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will limit the execution of the `test` and `build` steps to:

- builds with a branch of `master`
- builds with an event of `push`
  {{% /alert %}}

## Advanced

#### Fields

The following fields are used to configure the advanced version of the component:

| Name       | Description                                       | Required |
| ---------- | ------------------------------------------------- | -------- |
| `continue` | enables continuing the build if the step fails    | `false`  |
| `if`       | limits the step execution to all rules must match | `false`  |
| `matcher`  | matcher to use when evaluating the ruleset        | `false`  |
| `operator` | operator to use when evaluating the ruleset       | `false`  |
| `unless`   | limits the step execution to no rules can match   | `false`  |

#### Syntax

The following is an example of valid syntax for the advanced version of the component:

```diff
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
+    ruleset:
+      if:
+        branch: master
+        event: push
    commands:
      - go test ./...

  - name: build
    image: golang
+    ruleset:
+      unless:
+        branch: master
+        event: push
    commands:
      - go build
```

{{% alert color="info" %}}
This pipeline will limit the execution of the `test` step to:

- builds with a branch of `master`
- builds with an event of `push`

This pipeline will also limit the execution of the `build` step to:

- builds without a branch of `master`
- builds without an event of `push`
  {{% /alert %}}
