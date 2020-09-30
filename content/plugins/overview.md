---
title: "Overview"
linkTitle: "Overview"
description: >
  Learn about the kinds of Vela plugins.
---

{{% alert title="Note:" color="primary" %}}
Before you begin your plugin journey we recommend the following pre-requisites:

* [Steps](/docs/concepts/pipeline/steps/)
* [Stages](/docs/concepts/pipeline/stages/)
* [Templates](/docs/concepts/pipeline/templates/)
{{% /alert %}}

## Pipeline

These plugins are designed to be used within steps, stages and template pipelines. Pipeline plugins configuration works via environment variables that pass data from pipeline to the container at runtime. 

A pipeline plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, including:

* deploying code
* publishing artifacts
* sending notifications
* much, much more...

## Secret

{{% alert title="Note:" color="primary" %}}
Secret plugins are by default under an allow list of available images for an installation. To know which secret plugins are available for your Vela installation we recommend consulting your system administrators. 
{{% /alert %}}

These plugins are designed to be used within the secrets Yaml block of pipelines. Secret plugins configuration works via environment variables that pass data from pipeline to the container at runtime. 

A secret plugin works in tandem with the Vela workspace to read data from a provider and write them into an available location (`/vela/secrets`) within a pipeline.

## Using a plugin

Typically, plugins are configured as a step in a pipeline and should accept their configuration via environment variables. The below example shows a pipeline and secret plugin working together to publish an image to a registry:

```yaml
version: "1"

steps:
  - name: plugin
    image: target/vela-docker
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world

secrets:
  - name: vault_token

  - origin:
      name: plugin
      image: target/secret-vault
      pull: always
      secrets: [ vault_token ]
      parameters:
        addr: vault.company.com
        auth_method: token
        items:
          - source: secret/docker
            path: docker   
```

We pass these variables in Vela using the `parameters` block. Any variable passed to this block, will be injected into the step as `PARAMETER_<variable>`:

```diff
version: "1"

steps:
  - name: docker
    image: target/vela-docker
    pull: always
+   parameters:
+     registry: index.docker.io
+     repo: index.docker.io/octocat/hello-world

secrets:
  - name: vault_token

  - origin:
      name: vault
      image: target/secret-vault
      pull: always
      secrets: [ vault_token ]
+     parameters:
+       addr: vault.company.com
+       auth_method: token
+       items:
+         - source: secret/docker
+           path: docker  
```

From the above example, the following environment variables would be added to the containers:

**Docker:**

* `PARAMETER_REGISTRY=index.docker.io`
* `PARAMETER_REPO=index.docker.io/octocat/hello-world`

**Vault:**

* `PARAMETER_ADDR=index.docker.io`
* `PARAMETER_AUTH_METHOD=index.docker.io/octocat/hello-world`
* `PARAMETER_ITEMS={"items": [{"source": "secret/docker"}],"path": "docker"}`