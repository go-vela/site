---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list steps.
---

## Command

```
$ vela get step <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get step --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment    |
| -------- | -------------------- | -------------- |
| `org`    | name of organization | `BUILD_ORG`    |
| `repo`   | name of repository   | `BUILD_REPO`   |
| `build`  | number of build      | `BUILD_NUMBER` |
| `output` | format the output    | `N/A`          |

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
vela get step --org github --repo octocat --build-number 1
```

#### Response

```sh
NAME            STATUS  RUNTIME DURATION
publish         failure         1s
build           success         17s
test            success         10s
clone           success         2s
```
