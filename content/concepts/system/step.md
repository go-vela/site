---
title: "Step"
linkTitle: "Step"
description: >
  This section contains information on the step component in the system.
---

The `step` component is part of the core system components for Vela.

A `step` is defined as a sequential, execution instruction for a [pipeline](/docs/concepts/pipeline).

Each step is executed inside an ephemeral [Docker container](https://www.docker.com/resources/what-container) and are always executed in the order they are defined.

## Fields

The following fields make up this component:

| Name           | Type     | Description                                         |
| -------------- | -------- | --------------------------------------------------- |
| `build_id`     | `int64`  | unique identifier for build the step executed in    |
| `created`      | `int64`  | UNIX timestamp for when the step was created        |
| `distribution` | `string` | operating system the step was executed on           |
| `error`        | `string` | error message received during step execution time   |
| `exit_code`    | `int`    | return code received from the step execution        |
| `finished`     | `int64`  | UNIX timestamp for when the build was completed     |
| `host`         | `string` | hostname the step was executed on                   |
| `id`           | `int64`  | unique identifier for step in the system            |
| `image`        | `string` | Docker image used to create the step                |
| `name`         | `string` | unique name of the step for the build               |
| `number`       | `int`    | unique identifier for step for the build            |
| `repo_id`      | `int64`  | unique identifier for repo that triggered the build |
| `runtime`      | `string` | runtime the step was executed with                  |
| `started`      | `int64`  | UNIX timestamp for when the step was started        |
| `status`       | `string` | signifies the end condition for the step            |
| `stage`        | `string` | name of the stage the step was executed in          |

{{% alert color="info" %}}
This component is stored in the configured Vela backend in the `steps` table.
{{% /alert %}}

## References

* [API](/docs/api/step)
* [CLI](/docs/cli/step)
* SDK
  * [Go](/docs/sdk/go/step)
