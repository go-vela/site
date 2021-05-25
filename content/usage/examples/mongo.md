---
title: "Mongo"
toc: true
weight: 1
description: >
  Example Pipeline with Mongo
---

Example [Yaml](https://yaml.org/spec/) configuration for a project requiring a [Mongo](https://www.mongodb.com/) as a pipeline dependency.

## Scenario

User is looking to create a pipeline that can integrate with an ephemeral Mongo instance.

### Services

Services Yaml block can be used with stages and steps pipelines. This example uses a basic steps configuration.

The following [pipeline concepts](/docs/tour/) are being used in the pipeline below:

* [Services](/docs/tour/services/)
  * [Image](/docs/tour/image/)
* [Steps](/docs/tour/steps/)
  * [Image](/docs/tour/image/)
  * [Pull](/docs/tour/image/)
  * [Commands](/docs/tour/steps/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```diff
version: "1"
services:
  - name: mongo
    image: mongo:latest
    pull: always

steps:
  - name: check status
    image: mongo:latest
    pull: always
    commands:
      # sleeping can help ensure the service adequate time to start
+      - sleep 15
      - "mongo --host mongo --eval \"{ ping: 1 }\""
```

### Detach

If you're looking for more granular start time for the container you can add a detach flag within stages and steps pipelines.

The following [pipeline concepts](/docs/tour/) are being used in the pipeline below:

* [Steps](/docs/tour/steps/)
  * [Image](/docs/tour/image/)
  * [Pull](/docs/tour/image/)
  * [Commands](/docs/tour/steps/)

{{% alert title="Note:" color="primary" %}}
Pipeline must be stored in base of repository as `.vela.yml` or `.vela.yaml`

It is recommended to pin `image:` versions for production pipelines
{{% /alert %}}

```diff
version: "1"

steps:
  - name: mongo
    image: mongo:latest
    detach: true

  - name: check status
    image: mongo:latest
    commands:
      # sleeping can help ensure the service adequate time to start
+      - sleep 15
      - "mongo --host mongo --eval \"{ ping: 1 }\""
```
