---
title: "Pipeline"
linkTitle: "Pipeline"
description: >
  This section contains information on the pipeline components.
---

The `pipeline` component is a list of repeatable, execution instructions for Vela.

{{% alert color="info" %}}
A single, ephemeral run of a pipeline is known as a [build](/docs/concepts/resources/build).
{{% /alert %}}

It can be thought of as a defined workflow for how you test, build, and deploy your code.

This workflow is configured in a [YAML](https://yaml.org/) file found in the root of a repository.

{{% alert color="warning" %}}
The pipeline configuration, in the root of a repository, must be named as `.vela.yml` or `.vela.yaml`.
{{% /alert %}}

## Fields

The following fields are used to configure the component:

| Name        | Description                                                 | Required                  |
| ----------- | ----------------------------------------------------------- | ------------------------- |
| `metadata`  | extra information that can be passed to the pipeline        | `false`                   |
| `secrets`   | sensitive information to pass into the pipeline             | `false`                   |
| `services`  | detached (headless) execution instructions for the pipeline | `false`                   |
| `stages`    | parallel execution instructions for the pipeline            | `true` - with no `steps`  |
| `steps`     | sequential execution instructions for the pipeline          | `true` - with no `stages` |
| `templates` | pre-defined pipeline with variables for customization       | `false`                   |
| `version`   | syntax version used to evaluate the pipeline                | `true`                    |

{{% alert color="warning" %}}
All Vela pipelines will require either a `steps` or a `stages` declaration to be provided.

You **can not** provide both declarations in the same pipeline.
{{% /alert %}}

## Syntax

The following is an example of valid syntax for a `pipeline`:

```yaml
version: "1"

metadata:
  template: false

steps:
  - name: test
    image: golang
    commands:
      - go test ./...

  - name: build
    image: golang
    commands:
      - go build
```
