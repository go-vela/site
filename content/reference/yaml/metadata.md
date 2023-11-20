---
title: "Metadata"
linkTitle: "Metadata"
weight: 2
description: >
  YAML tags for metadata block
---

The metadata tag is intended to be used during the compile phase to signal how to treat the YAML document.

```yaml
---
# This document is displaying all the available tags
# in their default state for the compile process.
metadata:
  template: false
  clone: true
```

## Tags

| Tag             | Required | Type        | Description                                                        |
|-----------------|----------|-------------|--------------------------------------------------------------------|
| `template`      | Y        | bool        | Enables compiling the pipeline as a template.                      |
| `clone`         | N        | bool        | Enables injecting the default clone process.                       |
| `render_inline` | N        | bool        | Enables rendering without explicitly calling within the pipeline.  |
| `auto_cancel`   | N        | (see below) | Auto canceling settings for pipelines.                             | 

### Usage

#### The `template:` tag

{{% alert title="Tip:" color="info" %}}
To learn how to write templates, see the [template documentation](/docs/templates).
{{% /alert %}}

```yaml
---
metadata:
  # Enables compiling the pipeline as a template. This value 
  # is defaulted during the compile phase to "false" if not 
  # explicitly provided by the user.
  template: true
```

#### The `clone:` tag

```yaml
---
metadata:
  # Enables injecting the default clone process
  clone: true
```

#### The `environment:` tag

```yaml
---
metadata:
  # By default, the below is populated into every pipeline with
  # services, steps, and secrets. But, when the block exists the
  # configuration specified is used during compile phase.
  environment: [ steps, services, secrets ]
```

#### The `render_inline:` tag

```yaml
---
metadata:
  # By default, the below is populated into every pipeline with
  # false. But, when set to "true" a user can render a template 
  # in the resulting pipeline without referencing it in stages
  # or steps. 
  render_inline: false
```

#### The `auto_cancel` tag

| Tag              | Default  | Type  | Description                                                                                  |
|------------------|----------|-------|----------------------------------------------------------------------------------------------|
| `pending`        | True     | bool  | Pending builds will be auto canceled if qualifying build is triggered                        |
| `running`        | False    | bool  | Currently running builds will be auto canceled if qualifying build is triggered              |
| `default_branch` | False    | bool  | Pushes to the default branch will also be auto canceled if a qualifying build is triggered.  |

A **qualifying build** is defined as either:
  * a _push_ build with the same _branch_ as another running/pending _push_ build
  * a _pull request_ build with the same _head ref_ as another running/pending _pull request_ build

These builds most often happen when a user pushes a commit to a branch and quickly pushes another commit, both of which kick off new builds. Using the `auto_cancel` block can help free up build space and eliminate pointless builds.

By default, auto canceling is disabled altogether. However, if `running` or `default_branch` are specified, `pending` has a default value of `true` unless specified otherwise.

```yaml
---
# pending & running will auto cancel, but not pushes to the default branch.
metadata:
  auto_cancel:
    running: true 
```

```yaml
---
# running builds will auto cancel even if they are targeting the default branch, but pending builds will not.
metadata:
  auto_cancel:
    pending: false
    default_branch: true
    running: true
```