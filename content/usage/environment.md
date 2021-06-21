---
title: "Using the Environment"
toc: true
description: >
  Learn about how to leverage the environment within your builds.
---

Vela provides the ability to define environment variables scoped to individual steps, services and secrets. Additionally, if you need global environment setting you can set it at the parent and have it injected to all containers.

Please note the environment is design to be unique per container. Vela does inject a variety of default values from build, repo and user information.

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
+ environment:
+   GLOBAL_EXAMPLE: Hello, World Globally!
services:
  - name: redis
+   environment:
+     LOCAL_EXAMPLE: Hello, World!
    image: redis:latest

steps:
  - name: check status
    image: redis:latest
+   environment:
+     LOCAL_EXAMPLE: Hello, World!
    commands:
      # you can use bash commands in-line to set or override variables
      - export EXAMPLE="Hello World From Vela Team"
      - echo ${EXAMPLE}
      - echo ${GLOBAL_EXAMPLE}

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

## Global Usage

By default global injection effects all containers ran within the pipeline but if only want some container types to receive the configuration you can limit which types get them by adding the `environment` declaring into the metadata.

{{% alert title="Note:" color="primary" %}}
Valid values for metadata `environment:` YAML tag are `steps`, `services` and `secrets`.
{{% /alert %}}

```diff
version: "1"
+ environment:
+   GLOBAL_EXAMPLE: Hello, World Globally!

metadata:
  environment: [ steps ]

services:
  # Global configuration is no longer available in services
  - name: redis
+   environment:
+     LOCAL_EXAMPLE: Hello, World!
    image: redis:latest

steps:
  - name: check status
    image: redis:latest
+   environment:
+     LOCAL_EXAMPLE: Hello, World!
    commands:
      # you can use bash commands in-line to set or override variables
      - export EXAMPLE="Hello World From Vela Team"
      - echo ${EXAMPLE}
      - echo ${GLOBAL_EXAMPLE}

secrets:
  # Global configuration is no longer available in secrets
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