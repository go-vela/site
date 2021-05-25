---
title: "Rust (With Cargo)"
toc: true
weight: 1
description: >
  Example Rust (With Cargo) Pipeline
---

Example [Yaml](https://yaml.org/spec/) configuration for a project building a [Rust](https://www.rust-lang.org/) binary with [Cargo](https://doc.rust-lang.org/cargo/commands/cargo-doc.html).

## Scenario

User is looking to create a pipeline that builds an artifact on any event or branch pushed to source control.

### Steps

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Steps](/docs/concepts/pipeline/steps/)
  * [image](/docs/concepts/pipeline/steps/image/)
  * [Pull](/docs/concepts/pipeline/steps/pull/)
  * [Commands](/docs/concepts/pipeline/steps/commands/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

steps:
  - name: fetch
    image: rust:latest
    pull: always
    commands:
      - cargo fetch --verbose --all

  - name: test
    image: rust:latest
    pull: always
    environment:
      CGO_ENABLED: '0'
      GOOS: linux
    commands:
      - cargo test --verbose --all

  - name: build
    image: rust:latest
    pull: always
    environment:
      CGO_ENABLED: '0'
      GOOS: linux
    commands:
      - cargo build --verbose --all
```

### Stages

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Stages](/docs/concepts/pipeline/stages/)
  * [Needs](/docs/concepts/pipeline/stages/needs/)
  * [Steps](/docs/concepts/pipeline/steps/)
    * [image](/docs/concepts/pipeline/steps/image/)
    * [Pull](/docs/concepts/pipeline/steps/pull/)
    * [Commands](/docs/concepts/pipeline/steps/commands/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

stages:
  fetch:
    steps:
      - name: fetch
        image: rust:latest
        pull: always
        commands:
          - cargo fetch --verbose --all

  test:
    needs: [ fetch ]
    steps:
      - name: test
        image: rust:latest
        pull: always
        commands:
          - cargo test --verbose --all

  build:
    needs: [ fetch ]
    steps:
      - name: build
        image: rust:latest
        pull: always
        commands:
          - cargo build --verbose --all
```