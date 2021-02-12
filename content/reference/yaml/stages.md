---
title: "Stages"
linkTitle: "Stages"
weight: 7
description: >
  YAML stages for stages block
---

The `stages` tag is intended to be used to parallelize one-to-many sets of step tasks.

```yaml
---
# This document is displaying all the required tags
# to run two stages with one step task in parallel.
stages:
  test:
    hello:
      - name: Hello World
        image: alpine:latest
        commands:
          - echo "Hello, Vela User"

  welcome:
    steps:
      - name: Welcome to Vela
        image: alpine:latest
        commands:
          - echo "Welcome to Vela!"
```

## Tags

| Tag     | Required | Type     | Description                                               |
|---------|----------|----------|-----------------------------------------------------------|
| `name`  | Y        | string   | Unique identifier for the stage in the pipeline           |
| `steps` | Y        | []string | Sequential execution instructions for the stage           |
| `needs` | N        | struct   | Stages that must complete before starting the current one |

### Usage

#### The `name:` tag

```yaml
---
stages:
    # Unique identifier for the stage in the pipeline.
    welcome:
```

#### The `steps:` tag

```yaml
---
stages:
    # Unique identifier for the stage in the pipeline.
    welcome:
      # Sequential execution instructions for the stage.
      steps:
```

#### The `steps:` tag

{{% alert title="Tip:" color="info" %}}
For more details on steps tags, see the [step tags documentation](/docs/reference/yaml/steps/#tags)
{{% /alert %}}

```yaml
---
stages:
    greeting:

    # Unique identifier for the stage in the pipeline.
    welcome:
      # Stages that must complete before starting the current one.
      needs: [ greeting ]
```