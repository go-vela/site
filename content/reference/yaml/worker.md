---
title: "Worker"
linkTitle: "Worker"
weight: 3
description: >
  YAML tags for worker block
---

The worker tag is intended to be used to route a build to a specific worker pool of workers available with the Vela queue.

```yaml
---
# This document is displaying all the available tags
# and routing the build to a specific worker "sm:docker".
worker:
  flavor: sm
  platform: docker
```

{{% alert title="Warning:" color="warning" %}}
Routes are defined by the Vela system administrators during installation. To know what routes are available for your Vela installation, we recommend consulting your system administrators.
{{% /alert %}}

## Tags

| Tag        | Required | Type   | Description                                          |
|------------|----------|--------|------------------------------------------------------|
| `flavor`   | N        | string | Indicates what flavor of a worker. (i.e. sm, m, lg)    |
| `platform` | N        | string | Indicates the platform of a worker. (i.e. docker, k8s) |

### Usage

{{% alert title="Tip:" color="info" %}}
See an [example](/docs/usage/examples/route/) on how to route a build.
{{% /alert %}}

#### The `flavor:` tag

```yaml
---
worker:
  # indicates what flavor of worker (i.e. sm, m, lg). If not specified
  # will be scheduled in the generic "vela" queue.
  flavor: sm
```

#### The `platform:` tag

```yaml
---
worker:
  # Indicates the platform of worker (i.e. docker, k8s). If not specified
  # will be scheduled in the generic "vela" queue.
  platform: docker
```