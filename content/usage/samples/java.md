---
title: "Java"
toc: true
weight: 2
description: >
  Sample Java Pipeline
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
{{% /alert %}}

```yaml
version: "1"

steps:
  - name: install
    image: openjdk:8-alpine
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - ./gradlew downloadDependencies

  - name: test
    image: openjdk:8-alpine
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - ./gradlew test

  - name: build
    image: openjdk:8-alpine
    pull: true
    environment:
      GRADLE_USER_HOME: .gradle
      GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
    commands:
      - ./gradlew build
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
{{% /alert %}}

```yaml
version: "1"
stages:
  install:
    steps:
      - name: install
        image: openjdk:8-alpine
        pull: true
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - ./gradlew downloadDependencies
  test:
    needs: [ install ]
    steps:
      - name: test
        image: openjdk:8-alpine
        pull: true
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - ./gradlew test
          
  build:
    needs: [ install ]
    steps:
      - name: build
        image: openjdk:8-alpine
        pull: true
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - ./gradlew build
```