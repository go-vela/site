---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to add a worker (Vela Platform Admins only).
---

## Command

```
$ vela add worker <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela add worker --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name              | Description                      | Environment Variables                     |
| ----------------- | -------------------------------- | ----------------------------------------- |
| `worker.address`  | address of the worker            | `VELA_WORKER_ADDRESS`, `WORKER_ADDRESS`   |
| `worker.hostname` | hostname of the worker           | `VELA_WORKER_HOSTNAME`, `WORKER_HOSTNAME` |
| `output`          | format the output for the worker | `VELA_OUTPUT`, `WORKER_OUTPUT`            |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `output`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

## Permissions

Vela Platform Admin

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI and are authenticated as a Vela platform admin.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
$ vela add worker --worker.hostname MyWorker --worker.address myworker.example.com
```

#### Response generated from successful CLI command
```sh
worker registered successfully
```

## Examples

```sh
EXAMPLES:
  1. Add a worker reachable at the provided address.
    $ vela add worker --worker.hostname MyWorker --worker.address myworker.example.com
```