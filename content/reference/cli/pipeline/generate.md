---
title: "Generate"
linkTitle: "Generate"
description: >
  Learn how to produce a pipeline.
---

## Command

```
$ vela generate pipeline <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela generate pipeline --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                        | Environment Variables            |
| -------- | ---------------------------------- | -------------------------------- |
| `file`   | name of the file for the pipeline  | `VELA_FILE`, `PIPELINE_FILE`     |
| `path`   | path to the file for the pipeline  | `VELA_PATH`, `PIPELINE_PATH`     |
| `stages` | generates the pipeline with stages | `VELA_STAGES`, `PIPELINE_STAGES` |
| `type`   | type of pipeline being generated   | `VELA_TYPE`, `PIPELINE_TYPE`     |

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
vela generate pipeline
```

#### Response

```sh
".vela.yml" go pipeline generated
```
