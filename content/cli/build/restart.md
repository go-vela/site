---
title: "Restart"
linkTitle: "Restart"
description: >
  Learn how to rerun a build.
---

## Command

```
$ vela restart build <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela restart build --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment    |
| -------- | -------------------- | -------------- |
| `org`    | name of organization | `BUILD_ORG`    |
| `repo`   | name of repository   | `BUILD_REPO`   |
| `build`  | number of build      | `BUILD_NUMBER` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

* `org`
* `repo`

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
vela restart build --org github --repo octocat --build 1
```

#### Response

```sh
New build "github/octocat/2" was restarted from "github/octocat/1"
```
