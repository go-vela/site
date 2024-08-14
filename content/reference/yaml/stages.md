---
title: "Stages"
linkTitle: "Stages"
weight: 7
description: >
  YAML keys for stages block
---

The `stages` key is intended to be used to parallelize one-to-many sets of step tasks.

```yaml
---
# This document is displaying all the required keys
# to run two stages with one step task in parallel.
stages:
  hello:
    steps:
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

## Keys

| Key           | Required | Type     | Description                                                               |
|---------------|----------|----------|---------------------------------------------------------------------------|
| `name`        | Y        | string   | Unique identifier for the stage in the pipeline                           |
| `steps`       | Y        | []string | Sequential execution instructions for the stage                           |
| `needs`       | N        | []string | Stages that must complete before starting the current one                 |
| `independent` | N        | bool     | Stage will execute its steps and ignore failures from other stages' steps |

### Usage

#### The `name:` key

```yaml
---
stages:
    # Unique identifier for the stage in the pipeline.
    welcome:
```

#### The `steps:` key

```yaml
---
stages:
    # Unique identifier for the stage in the pipeline.
    welcome:
      # Sequential execution instructions for the stage.
      steps:
```

{{% alert title="Tip:" color="info" %}}
For more details on steps keys, see the [step keys documentation](/docs/reference/yaml/steps/#keys)
{{% /alert %}}

#### The `needs:` key

```yaml
---
stages:
    greeting:

    # Unique identifier for the stage in the pipeline.
    welcome:
      # Stages that must complete before starting the current one.
      needs: [ greeting ]
```

#### The `independent:` key

```yaml
---
stages:
    greeting:

    # Unique identifier for the stage in the pipeline.
    welcome:
      # If the greeting stage fails at any point, the welcome stage will continue its execution.
      independent: true
```
