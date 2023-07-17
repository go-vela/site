---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a worker.
---

## Command

```
$ vela view worker <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view worker --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name                        | Description                                                               | Environment Variables                                         |
| --------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------- |
| `worker.hostname`           | hostname of the worker                                                    | `VELA_WORKER_HOSTNAME`, `WORKER_HOSTNAME`                     |
| `worker.registration.token` | generate a registration token for the worker (requires Vela Platform Admin) | `VELA_WORKER_REGISTRATION_TOKEN`, `WORKER_REGISTRATION_TOKEN` |
| `output`                    | format the output for the repository                                      | `VELA_OUTPUT`, `WORKER_OUTPUT`                                |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `output`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
$ vela view worker --worker.hostname MyWorker
```

#### Response

```sh
id: 1
hostname: MyWorker
address: myworker.example.com
routes:
- vela
active: true
status: busy
laststatusupdatedat: 1681487969
runningbuildids:
- 123
lastbuildstartedat: 1681487969
lastbuildfinishedat: 1681487969
lastcheckedin: 1681487969
buildlimit: 1

```
