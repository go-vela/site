---
title: "Pipeline"
linkTitle: "Pipeline"
description: >
  Learn about pipeline plugins for Vela.
---

## Under the hood

Pipeline plugins are designed to automate, customize, and execute your software development workflows. The example we have shown is publishing an image to a registry:

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

## Building a plugin

The reason we use the environment for configuration is because it allows plugins to be written in any language! We have a number of tutorials that can help you get started in writing a plugin in your preferred language.

Before you get started writing a plugin you should have a good understanding of how Docker images are built. This will allow you to build a optimal plugin that follows [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).

{{% alert color="tip" %}}
We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}
