---
title: "Secrets"
linkTitle: "Secrets"
weight: 7
description: >
  Learn about secrets.
---

Sometimes you need to inject environment information into an image or plugin that you don't want in plain text in the pipeline file.

For this, we introduce pipeline secrets as a pattern to keep sensitive data safe.

Secrets are always retrieved at the beginning of a pipeline before any services, stages, or steps are created or started.

They are extremely useful when you don’t want to provide that sensitive information in plain text.

Let's go back to our Docker image used within the plugin tutorial and focus only on the repository secrets type. You can learn about all secret types in the [internal secrets example](/docs/usage/examples/secrets_internal/).

The pipeline we are looking at shows a few different patterns on how you can leverage adding and aliasing secrets in your pipeline.

However, this time we are going to remove the `username:` and `password:` YAML tags in the `parameter:` block and replace them with secrets within the container environment.

**See it in action with examples!**

* [internal secrets](/docs/usage/examples/internal_secrets/)
* [external secrets](/docs/usage/examples/external_secrets/)

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
    # where source is the name and target is the name of the env var.
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
  # This syntax is an implicit way of pulling a repo secret.
  # You can see all secret pattens in the reference section.
  - name: docker_password
  - name: password

  # Notice here I decided to use the explicit syntax. This allows
  # me to alias the name here instead of using source/target syntax
  # directly in the step
  - name: docker_username
    key: go-vela/docs/username
    engine: native
    type: repo
```

<!-- section break -->

**Tag references:**

[(step) `secrets:`](/docs/reference/yaml/steps/#the-secrets-tag), [(parent)  `secrets:`](/docs/reference/yaml/secrets),