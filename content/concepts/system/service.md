---
title: "Service"
linkTitle: "Service"
description: >
  This section contains information on the service component in the system.
---

The `service` component is part of the core system components for Vela.

A `service` is defined as a detached (headless), execution instruction for a [pipeline](/docs/concepts/pipeline).

Each service is executed inside an ephemeral [Docker container](https://www.docker.com/resources/what-container) and starts at the beginning of a pipeline.

## Fields

The following fields make up this component:

| Name           | Type     | Description                                          |
| -------------- | -------- | ---------------------------------------------------- |
| `build_id`     | `int64`  | unique identifier for build the service executed in  |
| `created`      | `int64`  | UNIX timestamp for when the service was created      |
| `distribution` | `string` | operating system the service was executed on         |
| `error`        | `string` | error message received during service execution time |
| `exit_code`    | `int`    | return code received from the service execution      |
| `finished`     | `int64`  | UNIX timestamp for when the build was completed      |
| `host`         | `string` | hostname the service was executed on                 |
| `id`           | `int64`  | unique identifier for service in the system          |
| `image`        | `string` | Docker image used to create the service              |
| `name`         | `string` | unique name of the service for the build             |
| `number`       | `int`    | unique identifier for service for the build          |
| `repo_id`      | `int64`  | unique identifier for repo that triggered the build  |
| `runtime`      | `string` | runtime the service was executed with                |
| `started`      | `int64`  | UNIX timestamp for when the service was started      |
| `status`       | `string` | signifies the end condition for the service          |

{{% alert color="info" %}}
This component is stored in the configured Vela backend in the `services` table.
{{% /alert %}}

## References

* [API](/docs/api/service)
* [CLI](/docs/cli/service)
* SDK
  * [Go](/docs/sdk/go/service)
