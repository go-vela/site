---
title: "Plugins"
linkTitle: "Plugins"
weight: 5
description: >
  Learn about plugin.
---

A plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, deploying code, publishing artifacts and more.

Anyone can create a plugin and use it in their pipeline. 

The registry of existing plugins can be found on this site in the [plugins](https://go-vela.github.io/docs/plugins/) tab.

Within the parameters block YAML tags are injected as upper case environment variables with the pattern of `PARAMETER_<YAML_TAG>`.

<!-- section break -->

```yaml
steps:

  - name: publish hello world
    image: target/vela-kaniko
    # Environment variables injected:
    # PARAMETER_REGISTRY=index.docker.io
    # PARAMETER_REPO=index.docker.io/go-vela/hello-world
    # PARAMETER_TAGS=latest,v1.0.0
    parameters:
      registry: index.docker.io
      repo: index.docker.io/go-vela/hello-world
      tags:
        - latest
        - v1.0.0
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`parameters:`](/docs/reference/yaml/steps/#the-parameters-tag), 