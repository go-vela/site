---
title: "Node"
toc: true
weight: 3
description: >
  Sample Node Pipeline
---

Sample [Yaml](https://yaml.org/spec/) configuration for a project building a [Node](https://nodejs.org/en/docs/) application.

## Scenario

User is looking to create a pipeline that builds an artifact on any event or branch pushed to source control.

### Steps

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Steps](/docs/concepts/pipeline/steps/)
* [image](/docs/concepts/pipeline/steps/image/)
* [Environment](/docs/concepts/pipeline/steps/environment/)
* [Pull](/docs/concepts/pipeline/steps/pull/)
* [Commands](/docs/concepts/pipeline/steps/commands/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

steps:
  - name: install
    image: node:latest
    pull: true
    commands:
      - node install

  - name: lint
    image: node:latest
    pull: true
    commands:
      - node test

  - name: build
    image: node:latest
    pull: true
    commands:
      - node build
```

### Stages

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Stages](/docs/concepts/pipeline/stages/)
* [Needs](/docs/concepts/pipeline/needs/)
* [Steps](/docs/concepts/pipeline/steps/)
* [image](/docs/concepts/pipeline/steps/image/)
* [Environment](/docs/concepts/pipeline/steps/environment/)
* [Pull](/docs/concepts/pipeline/steps/pull/)
* [Commands](/docs/concepts/pipeline/steps/commands/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

stages:
  install:
    steps:
      - name: install
        image: node:latest
        pull: true
        commands:
          - node install

  test:
    needs: [ install ]
    steps:
      - name: test
        image: node:latest
        pull: true
        commands:
          - node test

  build:
    needs: [ install ]
    steps:
      - name: build
        image: node:latest
        pull: true
        commands:
          - node build
```