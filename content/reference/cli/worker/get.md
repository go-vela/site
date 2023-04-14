---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list workers.
---

## Command

```
$ vela get workers <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get workers --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                          | Environment Variables              |
| ---------- | ------------------------------------ | ---------------------------------- |
| `output`   | format the output for the workers    | `VELA_OUTPUT`, `WORKER_OUTPUT`     |

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
$ vela get workers
```

#### Response generated from successful CLI command
```sh
HOSTNAME	ACTIVE	ROUTES	LAST_CHECKED_IN
MyWorker1  	true  	[vela]	1681485812
MyWorker2  	true  	[vela]	1681485814
```

## Examples

```sh
EXAMPLES:
  1. Get a list of workers.
    $ vela get worker
  2. Get a list of workers with wide view output.
    $ vela get worker --output wide
  3. Get a list of workers with yaml output.
    $ vela get worker --output yaml
  4. Get a list of workers with json output.
    $ vela get worker --output json
  5. Get a list of workers when config or environment variables are set.
    $ vela get worker
```
