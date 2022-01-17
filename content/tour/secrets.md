---
title: "Secrets"
linkTitle: "Secrets"
weight: 7
description: >
  Learn about secrets.
---

Sometimes you need to inject environment information into an image or plugin that you don't want in plain text.

For this, we introduce pipeline secrets as a pattern to keep sensitive data safe. Secrets are always retrieved at the beginning of a pipeline before any services, stages, or steps are created or started.

They are the answer when you don’t want to provide that sensitive information in plain text.

Let's go back to our Docker image used within the plugin tutorial and focus only on the repository secrets type. You can learn about all secret types in the [secrets usage section](/docs/usage/secrets/).

The pipeline we are looking at shows a few different patterns on how you can leverage adding and aliasing secrets in your pipeline.

However, this time we are going to remove the `username:` and `password:` YAML tags in the `parameter:` block and replace them with secrets within the container environment.

**See it in action with examples!**

* [internal secrets](/docs/usage/examples/secrets_internal/)
* [external secrets](/docs/usage/examples/secrets_external/)

<!-- section break -->

```yaml
steps:
  - name: publish hello world
    image: target/vela-kaniko
    # Here we simply just match the key with the plugin then
    # when the container starts you will get "DOCKER_PASSWORD=<value>"
    # in the container environment
    secrets: [ docker_password ]
    parameters:
      registry: index.docker.io
      repo: index.docker.io/go-vela/hello-world
      username: moby
      tags:
        - latest
        - v1.0.0

  - name: publish hello world
    image: target/vela-kaniko
    # Now lets try something more complicated let's say you want to
    # alias your secret. You can do that via source and target syntax
    # where source is the new name and target is the name of the env var.
    secrets:
      - source: password
        target: docker_password
      - source: docker_username
        target: docker_username
    parameters:
      registry: index.docker.io
      repo: index.docker.io/go-vela/hello-world
      tags:
        - latest
        - v1.0.0

secrets:
  # Notice here how the name and the key don't need to match.
  # This gives end users an ability to reuse or rename secrets with
  # different names across their various pipelines. This is similar
  # to the alias above, but allows for aliasing across the entire pipeline.
  - name: docker_username
    key: go-vela/docs/username
    engine: native
    type: repo
```

<!-- section break -->

**Tag references:**

[(step) `secrets:`](/docs/reference/yaml/steps/#the-secrets-tag), [(parent)  `secrets:`](/docs/reference/yaml/secrets),
