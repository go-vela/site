---
title: "Using the Environment"
toc: true
description: >
  Learn about how to leverage the environment within your builds.
---

Vela provides the ability to define environment variables scoped to individual steps, services and secrets. Pleas note the environment is design to be unique per container. Vela does inject a variety of default values from build, repo and user information.

Defaults:

* [Services](https://go-vela.github.io/docs/concepts/pipeline/services/environment/#defaults)
* [Steps](https://go-vela.github.io/docs/concepts/pipeline/steps/environment/#defaults)

## Usage

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Services](/docs/concepts/pipeline/services/)
  * [Environment](/docs/concepts/pipeline/steps/environment/)
* [Steps](/docs/concepts/pipeline/steps/)
  * [Environment](/docs/concepts/pipeline/steps/environment/)
* [Secrets](/docs/concepts/pipeline/secrets/)
  * [Origin](/docs/concepts/pipeline/secrets/origin/)

{{% alert title="Note:" color="primary" %}}
Please be warned that `${variable}` expressions are subject to pre-processing.

If you do not want the pre-processor to evaluate your expression it must be escaped.
{{% /alert %}}

```diff
version: "1"
services:
  - name: redis
+   environment:
+     EXAMPLE: Hello, World!
    image: redis:latest

steps:
  - name: check status
    image: redis:latest
+   environment:
+     EXAMPLE: Hello, World!
    commands:
      # you can use bash commands in-line to set or override variables
      - export EXAMPLE="Hello World From Vela Team"
      - echo ${EXAMPLE}

secrets:
  - origin:
      name: private vault
      image: target/secret-vault:latest
+     environment:
+       EXAMPLE: Hello, World!
      secrets: [ vault_token ]
      parameters:
        addr: vault.example.com
        auth_method: token
        username: octocat
        items:
          - source: secret/docker
            path: docker
```
