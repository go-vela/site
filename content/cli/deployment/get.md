---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list deployments.
---

## Command

```
$ vela get deployment <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get deployment --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment |
| -------- | -------------------- | ----------- |
| `org`    | name of organization | `VELA_ORG`  |
| `repo`   | name of repository   | `VELA_REPO` |
| `output` | format the output    | `N/A`       |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`

For more information, please review the [CLI config documentation](/docs/cli/config/).
{{% /alert %}}

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
vela get deployment --org github --repo octocat
```

#### Response

```sh
ID  TASK         USER     REF     TARGET
2   deploy:vela  octocat  master  production
1   deploy:vela  octocat  master  production
```
