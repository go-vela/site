---
title: "Internal Secrets"
toc: true
weight: 1
description: >
  Example Pipeline with internal secrets
---

Example [Yaml](https://yaml.org/spec/) configuration for a project requiring a secrets to be used within a step

## Scenario

User is looking to create a pipeline that can inject configuration that can not be placed into a Yaml file. A simple example would be producing a Docker image with username and password.

{{% alert title="Note:" color="primary" %}}
It is assumed you have created secrets `docker_username` and `docker_password` in the web interface or [CLI](/docs/cli/).
{{% /alert %}}

The examples show a pipeline using repository secrets. Vela contains three secret types: repository, organization, and shared. For examples on organization and shared, please see the [secret concepts](/docs/concepts/pipeline/steps/secrets/) documentation.

### Steps

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Steps](/docs/concepts/pipeline/steps/)
  * [Image](/docs/concepts/pipeline/steps/image/)
  * [Pull](/docs/concepts/pipeline/steps/pull/) 
  * [Secrets](/docs/concepts/pipeline/steps/secrets/)
  * [Parameters](/docs/concepts/pipeline/steps/parameters/)
* [Secrets](/docs/concepts/pipeline/secrets/)

The following [Vela plugins](/docs/concepts/pipeline) are being used in the pipeline below:

* [Docker](/docs/plugins/pipeline/registry/docker/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

steps:
  - name: publish hello world
    image: target/vela-docker:latest
    pull: always
    secrets: [ docker_username, docker_password ]
    parameters:
      registry: index.docker.io
      repo: index.docker.io/vela/hello-world


secrets:
  # Implicit secret definition. This definition is only supported for native secrets of repository type.
  - name: docker_username

  # Declarative secret definition.
  - name: foo1
    key: vela/hello-world/docker_password
    engine: native
    type: repo
```

### Stages

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Stages](/docs/concepts/pipeline/steps/)
  * [Steps](/docs/concepts/pipeline/steps/)
  * [Image](/docs/concepts/pipeline/steps/image/)
  * [Pull](/docs/concepts/pipeline/steps/pull/)
  * [Secrets](/docs/concepts/pipeline/steps/secrets/)
  * [Parameters](/docs/concepts/pipeline/steps/parameters/)
* [Secrets](/docs/concepts/pipeline/secrets/)

The following [Vela plugins](/docs/concepts/pipeline) are being used in the pipeline below:

* [Docker](/docs/plugins/pipeline/registry/docker/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```yaml
version: "1"

stages:
  docker:
    steps:
      - name: publish hello world
        image: target/vela-docker:latest
        pull: always
        secrets: [ docker_username, docker_password ]
        parameters:
          registry: index.docker.io
          repo: index.docker.io/vela/hello-world

secrets:
  # Implicit secret definition. This definition is only supported for native secrets of repository type.
  - name: docker_username

  # Declarative secret definition.
  - name: foo1
    key: vela/hello-world/docker_password
    engine: native
    type: repo   
```
