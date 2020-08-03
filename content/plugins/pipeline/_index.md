---
title: "Pipeline"
linkTitle: "Pipeline"
description: >
  Learn about pipeline plugins for Vela.
---
## Using a plugin

Typically, plugins are configured as a step in a pipeline and should accept their configuration via environment variables. The below example shows a Docker plugin that can publish an image to a registry:

```yaml
version: "1"

steps:
  - name: plugin
    image: target/vela-docker:v0.1.0
    pull: true
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

We pass these variables in Vela using the `parameters` block. Any variable passed to this block, will be injected into the step as `PARAMETER_<variable>`:

```diff
version: "1"

steps:
  - name: plugin
    image: target/vela-docker:v0.1.0
    pull: true
+   parameters:
+     registry: index.docker.io
+     repo: index.docker.io/octocat/hello-world
```

From the above example, the following environment variables would be added to the container:

* `PARAMETER_REGISTRY=index.docker.io`
* `PARAMETER_REPO=index.docker.io/octocat/hello-world`

## Building a plugin

The reason we use the environment for configuration is because it allows plugins to be written in any language! We have a number of tutorials that can help you get started in writing a plugin in your preferred language.

Before you get started writing a plugin you should have a good understanding of how Docker images are built. This will allow you to build a optimal plugin that follows [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).

{{% alert color="tip" %}}
We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}
