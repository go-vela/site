---
title: "Overview"
linkTitle: "Overview"
description: >
  Learn about plugins for Vela.
---

A plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, including:

* deploying code
* publishing artifacts
* sending notifications
* much, much more...

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

{{% alert color="warning" %}}
We recommend you review [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create your own plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Configuration

Typically, plugins are configured as a step in a pipeline and should accept their configuration via environment variables.

{{% alert color="info" %}}
This has the added benefit of allowing plugins to be written in any language!
{{% /alert %}}

We pass these variables in Vela using the `parameters` block. Any variable passed to this block, will be injected into the step as `PARAMETER_<thing>`:

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

From the above example, the following environment variables would be added:

* `PARAMETER_REGISTRY=index.docker.io`
* `PARAMETER_REPO=index.docker.io/octocat/hello-world`
