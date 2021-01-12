---
title: "Plugins"
linkTitle: "Plugins"
layout: plugins
description: >
  This section contains information on how to use Vela plugins.
menu:
  main:
    weight: 305
---

Vela contains two plugin types pipeline and secret. Both accept configuration via environment variables but should be used within their specific location of the Yaml pipeline. Pipeline plugins are designed to be used within steps, stages, and template pipelines. Secret plugins are designed to be used within the secrets Yaml block of pipelines.

{{% alert title="Note:" color="warning" %}}
Before you begin your plugin journey we recommend the following pre-requisites:

* [Steps](/docs/concepts/pipeline/steps/)
* [Stages](/docs/concepts/pipeline/stages/)
* [Templates](/docs/concepts/pipeline/templates/)
{{% /alert %}}

## Pipeline

Pipeline plugins are designed to automate, customize, and execute your software development workflows. A pipeline plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, including:

* deploying code
* publishing artifacts
* sending notifications
* much, much more...

### Sample

The sample we have shown is publishing an image to a registry:Pipeline plugins configuration works via environment variables that pass data from pipeline to the container at runtime. 

_Not a runnable pipeline_
```diff
version: "1"

steps:
  - name: docker
    image: target/vela-docker
    pull: always
+   parameters:
+     registry: index.docker.io
+     repo: index.docker.io/octocat/hello-world
```

## Secret

{{% alert title="Note:" color="warning" %}}
Secret plugins are configured with an allow list of available images via an administator on installation. To know which secret plugins are available for your Vela installation we recommend consulting your system administrators. 
{{% /alert %}}

Secret plugins are designed to be used to read secrets in volumes within the Vela workspace. When a secret plugin runs the plugin should write data to the custom Vela mount (`/vela/secrets/`) as key/value pairs. Secret plugins configuration works via environment variables that pass data from pipeline to the container at runtime. 

A secret plugin works in tandem with the Vela workspace to read data from a provider and write them into an available location (`/vela/secrets`) within a pipeline.

### Sample

_Not a runnable pipeline_
```diff
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
+       username: octocat
+       items:
+         - source: secret/docker
+           path: docker  
```

From the above example, will have written the following available secrets to:

* `/vela/secrets/docker/<key>/<value/`
