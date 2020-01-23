---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list builds.
---

## Command

```
$ vela get build <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get build --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment  |
| -------- | -------------------- | ------------ |
| `org`    | name of organization | `BUILD_ORG`  |
| `repo`   | name of repository   | `BUILD_REPO` |
| `output` | format the output    | `N/A`        |

{{% alert color="info" %}}
This command also supports setting the `org` or `repo` parameters via a configuration file.

For more information, please review the [CLI config documentation](/docs/cli/config).
{{% /alert %}}

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/cli/install).

To setup the CLI, please review the [authentication documentation](/docs/cli/authentication).
{{% /alert %}}

#### Request

```sh
vela get build --org github --repo octocat
```

#### Response

```sh
NUMBER  STATUS  EVENT   BRANCH  DURATION
5       failure push    master  45s
4       failure push    master  50s
3       success push    master  54s
2       success push    master  55s
1       pending push    master  ...
```
