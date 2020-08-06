---
title: "Validate"
linkTitle: "Validate"
description: >
  Learn how to validate a Vela pipeline.
---

## Command

```
$ vela validate pipeline <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, please run `vela validate pipeline --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                        | Environment Variables            |
| -------- | ---------------------------------- | -------------------------------- |
| `file`   | name of the file for the pipeline  | `VELA_FILE`, `PIPELINE_FILE`     |
| `path`   | path to the file for the pipeline  | `VELA_PATH`, `PIPELINE_PATH`     |

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/cli/install/).
To setup the CLI, please review the [authentication documentation](/docs/cli/authentication/).
{{% /alert %}}

#### Request

```sh
vela validate pipeline
```

#### Response

```sh
".vela.yml" is valid
```
