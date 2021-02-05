---
title: "Plugins"
linkTitle: "Plugins"
weight: 4
description: >
  Learn about plugin.
---

A plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, deploying code, publishing artifacts and more.

Anyone can create a plugin and use it in their pipeline. 

The registry of existing plugins can be found on this site in the [plugins](https://go-vela.github.io/docs/plugins/) tab.

<!-- section break -->

```yaml
steps:
  - name: publish hello world
    image: target/vela-kaniko
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`parameters:`](/docs/reference/yaml/steps/#the-parameters-tag), 