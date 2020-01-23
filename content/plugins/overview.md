---
title: "Overview"
linkTitle: "Overview"
description: >
  Learn about plugins for Vela.
---

A plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, including but not limited to, deploying code, publishing artifacts, and sending notifications.

```yaml
version: "1"

steps:
  image: target/vela-docker:v0.1.0
  pull: true
  parameters:
    registry: index.docker.io
    repo: index.docker.io/octocat-hello-world
```

{{% alert color="warning" %}}
We recommend you review [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create your own plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

Typically, plugins are configured as a step in a pipeline and should accept their configuration via environment variables.

Due to plugins being executed in Docker containers and accepting their configuration via environment variables, this allows them to be written in any language
