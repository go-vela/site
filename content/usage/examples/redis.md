---
title: "Redis"
toc: true
weight: 1
description: >
  Example Pipeline with Redis
---

Example [Yaml](https://yaml.org/spec/) configuration for a project requiring a [Redis](https://redis.io/) as a pipeline dependency.

## Scenario

User is looking to create a pipeline that can integrate with an ephemeral Redis instance.

### Services

Services Yaml block can be used with stages and steps pipelines. This example uses a basic steps configuration.

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Services](/docs/concepts/pipeline/services/)
  * [Image](/docs/concepts/pipeline/services/image/)
* [Steps](/docs/concepts/pipeline/steps/)
  * [Image](/docs/concepts/pipeline/steps/image/)
  * [Pull](/docs/concepts/pipeline/steps/pull/)
  * [Commands](/docs/concepts/pipeline/steps/commands/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```diff
version: "1"
services:
  - name: redis
    image: redis:latest
    pull: always

steps:
  - name: check status
    image: redis:latest
    pull: always
    commands:
      # sleeping can help ensure the service adequate time to start
+      - sleep 15
      - redis-cli -h redis ping
```

### Detach

If you're looking for more granular start time for the container you can add a detach flag within stages and steps pipelines.

The following [pipeline concepts](/docs/concepts/pipeline) are being used in the pipeline below:

* [Steps](/docs/concepts/pipeline/steps/)
  * [Image](/docs/concepts/pipeline/steps/image/)
  * [Pull](/docs/concepts/pipeline/steps/pull/)
  * [Commands](/docs/concepts/pipeline/steps/commands/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```diff
version: "1"

steps:
  - name: redis
    image: redis:latest
    pull: always
    detach: true

  - name: check status
    image: redis:latest
    pull: always
    commands:
      # sleeping can help ensure the service adequate time to start
+      - sleep 15
      - redis-cli -h redis ping
```