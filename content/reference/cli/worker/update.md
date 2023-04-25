---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a worker.
---

## Command

```
$ vela update worker <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update worker --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name              | Description                              | Environment Variables                           |
| ----------------- | ---------------------------------------- | ----------------------------------------------- |
| `worker.address`  | address of the worker                    | `VELA_WORKER_ADDRESS`, `WORKER_ADDRESS`         |
| `worker.hostname` | hostname of the worker                   | `VELA_WORKER_HOSTNAME`, `WORKER_HOSTNAME`       |
| `active`          | current status of the worker (unused)    | `VELA_WORKER_ACTIVE`, `WORKER_ACTIVE`           |
| `build-limit`     | build limit for the worker (ignored)     | `VELA_WORKER_BUILD_LIMIT`, `WORKER_BUILD_LIMIT` |
| `routes`          | route assignment for the worker (unused) | `VELA_WORKER_ROUTES`, `WORKER_ROUTES`           |
| `output`          | format the output for the worker         | `VELA_OUTPUT`, `WORKER_OUTPUT`                  |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `output`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

## Permissions

Vela Platform Admin

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
$ vela update worker --worker.address newaddress.example.com
```

{{% alert color="info" %}}
Not passing `--worker.hostname` will automatically use the hostname part of the passed in `--worker.address` as the hostname.
{{% /alert %}}

#### Response

```sh
{
  ID: 1,
  Hostname: MyWorker,
  Address: newaddress.example.com,
  Routes: [vela],
  Active: true,
  LastCheckedIn: 1681486769,
  BuildLimit: 1,
}
```
