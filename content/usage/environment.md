---
title: "Using the Environment"
toc: true
description: >
  Learn about how to leverage the environment within your builds.
---

Vela provides the ability to define environment variables scoped to individual steps, services and secrets. Pleas note the environment is design to be unique per container. Vela does inject a variety of default values from build, repo and user information.

Defaults:

* [Container](/docs/reference/environment/variables/#container-defaults)
* [Steps only](/docs/reference/environment/variables/#step-only-defaults)
* [Services only](/docs/reference/environment/variables/#service-only-defaults)

## Usage

The following [pipeline concepts](/docs/tour) are being used in the pipeline below:

* [Services](/docs/tour/services/)
  * [Environment](/docs/tour/environment/)
* [Steps](/docs/tour/steps/)
  * [Environment](/docs/tour/environment/)
* [Secrets](/docs/tour/secrets/)
  * [Origin](/docs/tour/secrets/)

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
