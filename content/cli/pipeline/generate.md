---
title: "Generate"
linkTitle: "Generate"
description: >
  Learn how to produce a pipeline.
---

## Command

```
$ vela generate pipe <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela generate pipe --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                            | Environment |
| -------- | -------------------------------------- | ----------- |
| `type`   | language of pipeline to generate       | `N/A`       |
| `path`   | output path to pipeline                | `N/A`       |
| `stages` | enable generating pipeline with stages | `N/A`       |

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
vela generate pipe
```

#### Response

```sh
".vela.yml" go pipeline generated
```
