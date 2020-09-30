---
title: "External Secrets"
toc: true
weight: 1
description: >
  Sample pipeline with external secrets
---

Sample [Yaml](https://yaml.org/spec/) configuration for a project requiring a secrets to be used within a step

## Scenario

User is looking to create a pipeline that can integrate with a private Vault to inject secrets that can not be used with pushing a Docker image to a registry.

{{% alert title="Note:" color="primary" %}}
It is assumed you have created secret `vault_token` in the web interface or [CLI](/docs/cli/).
{{% /alert %}}

The samples show a pipeline using repository secrets. Vela contains three secret types: repository, organization, and shared. For examples on organization and shared, please see the [secret concepts](/docs/concepts/pipeline/steps/secrets/) documentation.

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
    parameters:
      registry: index.docker.io
      repo: index.docker.io/vela/hello-world


secrets:
  # Implicit secret definition.
  - name: vault_token

  - origin:
      name: private vault
      image: target/secret-vault:latest
      pull: always
      secrets: [ vault_token ]
      parameters:
        addr: vault.example.com
        auth_method: token
        username: octocat
        items:
          - source: secret/docker
            path: docker  
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

worker:
  runtime: docker

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
  # Implicit secret definition.
  - name: vault_token

  - origin:
      name: private vault
      image: target/secret-vault:latest
      pull: always
      secrets: [ vault_token ]
      parameters:
        addr: vault.example.com
        auth_method: token
        username: octocat
        items:
          - source: secret/docker
            path: docker  
```