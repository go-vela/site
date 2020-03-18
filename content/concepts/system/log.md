---
title: "Log"
linkTitle: "Log"
description: >
  This section contains information on the log component in the system.
---

The `log` component is part of the core system components for Vela.

A `log` is defined as a sequence of records about the actions performed by a worker in a [build](/docs/concepts/system/build/).

## Fields

The following fields make up this component:

| Name         | Type     | Description                                         |
| ------------ | -------- | --------------------------------------------------- |
| `build_id`   | `int64`  | unique identifier for build the log entry is for    |
| `data`       | `[]byte` | raw data from the log entry                         |
| `id`         | `int64`  | unique identifier for log in the system             |
| `repo_id`    | `int64`  | unique identifier for repo that triggered the build |
| `service_id` | `int64`  | unique identifier for service the log entry is for  |
| `step_id`    | `int64`  | unique identifier for step the log entry is for     |

{{% alert color="info" %}}
This component is stored in the configured Vela backend in the `logs` table.
{{% /alert %}}

## References

- API
  - [Build](/docs/api/build/logs/)
  - [Service](/docs/api/service/logs/)
  - [Step](/docs/api/step/logs/)
- [CLI](/docs/cli/log/)
- SDK
  - Go
    - [Build](/docs/sdk/go/build/logs/)
    - [Service](/docs/sdk/go/service/logs/)
    - [Step](/docs/sdk/go/step/logs/)
