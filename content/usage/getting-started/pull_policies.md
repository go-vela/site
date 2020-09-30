---
title: "Pull Policies"
toc: true
weight: 8
description: >
  Learn how to control pulling images in your pipeline.
---

Vela provides the ability to define how and when the images for secrets, steps, and services will be retrieved at runtime.

## Usage

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Services](/docs/concepts/pipeline/services/)
  * [Pull](/docs/concepts/pipeline/services/pull/)
* [Steps](/docs/concepts/pipeline/steps/)
  * [Pull](/docs/concepts/pipeline/steps/pull/)
* [Secrets](/docs/concepts/pipeline/secrets/)
  * [Origin](/docs/concepts/pipeline/steps/origin/)

{{% alert title="Note:" color="primary" %}}
Please be warned that the `pull` declaration is **not required**.

If you do not provide the `pull` declaration, a default value of `not_present` will be used.
{{% /alert %}}

```diff
version: "1"
services:
  - name: redis
    image: redis:latest
+   pull: always

steps:
  - name: check status
    image: alpine:latest
+   pull: not_present
    commands:
      # you can use bash commands in-line to set or override variables
      - export EXAMPLE="Hello World From Vela Team"
      - echo ${EXAMPLE}

secrets:
  - origin:
      name: private vault
      image: target/secret-vault:latest
+     pull: on_start
      secrets: [ vault_token ]
      parameters:
        addr: vault.example.com
        auth_method: token
        username: octocat
        items:
          - source: secret/docker
            path: docker
```

{{% alert color="info" %}}
This pipeline will:

* always attempt to pull the `redis:latest` image, even if it exists locally
* only pull the `alpine:latest` image if it doesn't already exist locally
* wait to pull the `target/secret-vault:latest` image until right before starting the container
{{% /alert %}}