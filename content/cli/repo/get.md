---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list repos.
---

## Command

```
$ vela get repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description       | Environment |
| -------- | ----------------- | ----------- |
| `output` | format the output | `N/A`       |

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
vela get repo
```

#### Response

```sh
ORG/REPO        STATUS  EVENTS             VISIBILITY  BRANCH
github/octocat  true    push,pull_request  public      master
```
