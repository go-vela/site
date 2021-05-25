---
title: "Java (With Maven)"
toc: true
weight: 2
description: >
  Example Java (With Maven) Pipeline
---

Example [Yaml](https://yaml.org/spec/) configuration for a project building a [Java](https://docs.oracle.com/en/java/) application with [Maven](https://maven.apache.org/guides/index.html).

## Scenario

User is looking to create a pipeline that builds an artifact on any event or branch pushed to source control.

### Steps

The following [pipeline concepts](/docs/tour/) are being used in the pipeline below:

* [Steps](/docs/tour/steps/)
  * [image](/docs/tour/image/)
  * [Environment](/docs/tour/environment/)
  * [Pull](/docs/tour/image/)
  * [Commands](/docs/tour/steps/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

steps:
  - name: install
    image: maven:latest
    pull: always
    commands:
      - mvn install

  - name: test
    image: maven:latest
    pull: always
    commands:
      - mvn test

  - name: build
    image: maven:latest
    pull: always
    commands:
      - mvn package
```

### Stages

The following [pipeline concepts](/docs/tour) are being used in the pipeline below:

* [Stages](/docs/tour/stages/)
  * [Needs](/docs/tour/stages/)
  * [Steps](/docs/tour/steps/)
    * [image](/docs/tour/image/)
    * [Environment](/docs/tour/environment/)
    * [Pull](/docs/tour/image/)
    * [Commands](/docs/tour/steps/)

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
        image: maven:latest
        pull: always
        commands:
          - mvn install
  test:
    needs: [ install ]
    steps:
      - name: test
        image: maven:latest
        pull: always
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - mvn test
          
  build:
    needs: [ install ]
    steps:
      - name: build
        image: maven:latest
        pull: always
        environment:
          GRADLE_USER_HOME: .gradle
          GRADLE_OPTS: -Dorg.gradle.daemon=false -Dorg.gradle.workers.max=1 -Dorg.gradle.parallel=false
        commands:
          - mvn package
```