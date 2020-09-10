---
title: "Java (With Gradle)"
toc: true
weight: 2
description: >
  Sample Java (With Gradle) Pipeline
---

Sample [Yaml](https://yaml.org/spec/) configuration for a project building a [Java](https://docs.oracle.com/en/java/) application with [Gradle](https://docs.gradle.org/current/userguide/userguide.html).

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
    image: gradle:latest
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - gradle downloadDependencies

  - name: test
    image: gradle:latest
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - gradle test

  - name: build
    image: gradle:latest
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - gradle build
```

### Stages

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Stages](/docs/concepts/pipeline/stages/)
  * [Needs](docs/concepts/pipeline/stages/needs/)
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
        image: gradle:latest
        pull: true
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - gradle downloadDependencies
  test:
    needs: [ install ]
    steps:
      - name: test
        image: gradle:latest
        pull: true
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - gradle test
          
  build:
    needs: [ install ]
    steps:
      - name: build
        image: gradle:latest
        pull: true
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - gradle build
```