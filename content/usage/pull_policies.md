---
title: "Pull Policies"
toc: true
description: >
  Learn how to control pulling images in your pipeline.
---

Vela provides the ability to define how and when the images for secrets, steps, and services will be retrieved at runtime.

## Usage

Below are the options for pull policies for container images

| Policy          | Description                                                     |
|---------------  |-----------------------------------------------------------------|
| `always`        | Always attempt to pull image from registry, even if it exists locally. Best used when leveraging a mutable tag, such as `latest`            |
| `not_present`   | Only attempt to pull image from registry if it does not already exist locally. This is the default behavior and is recommended for immutably tagged images.              |
| `on_start`      | Pull image from registry right before the step is to be executed. Can speed up build times if the step or service does not run on every build (e.g. failed build notifying plugins), can be leveraged when dealing with password rotation mid-build (e.g. Vault plugin), or can be used to pull an image that was created and published earlier in the build. |
| `never`         | Only use images that exist locally.              |

{{% alert title="Note:" color="primary" %}}
The `pull` declaration is **not required**.

If you do not provide the `pull` declaration, a default value of `not_present` will be used.
{{% /alert %}}

## Example

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

## References

The following [pipeline concepts](/docs/tour) are being used in the pipeline below:

* [Services](/docs/tour/services/)
  * [Pull](/docs/tour/image/)
* [Steps](/docs/tour/steps/)
  * [Pull](/docs/tour/image/)
* [Secrets](/docs/tour/secrets/)
  * [Origin](/docs/tour/secrets/)

* [`Pull` YAML Key](/docs/reference/yaml/steps/#the-pull-key)

