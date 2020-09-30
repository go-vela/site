---
title: "Postgres"
toc: true
weight: 1
description: >
  Sample Pipeline with Postgres
---

Sample [Yaml](https://yaml.org/spec/) configuration for a project requiring a [Postgres](https://www.postgresql.org/) as a pipeline dependency.

## Scenario

User is looking to create a pipeline that can integrate with an ephemeral Postgres instance.

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
  - name: postgres
    image: postgres:latest
    pull: always
    environment:
      POSTGRES_USER: admin
      POSTGRES_DB: vela

steps:
  - name: check status
    image: postgres:latest
    pull: always
    commands:
      # sleeping can help ensure the service adequate time to start
+      - sleep 15
      - psql -U admin -d vela -h tcp://postgres:5432
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
  - name: postgres
    image: postgres:latest
    pull: always
    environment:
      POSTGRES_USER: admin
      POSTGRES_DB: vela    
    detach: true

  - name: check status
    image: postgres:latest
    pull: always
    commands:
      # sleeping can help ensure the service adequate time to start
+      - sleep 15
      - psql -U admin -d vela -h tcp://postgres:5432
```
