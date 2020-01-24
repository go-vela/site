---
title: "Chown"
linkTitle: "Chown"
description: >
  Learn how to change ownership of a repo.
---

## Command

```
$ vela chown repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela chown repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment |
| -------- | -------------------- | ----------- |
| `org`    | name of organization | `REPO_ORG`  |
| `repo`   | name of repository   | `REPO_NAME` |
| `output` | format the output    | `N/A`       |

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
vela chown repo --org github --repo octocat
```

#### Response

```sh
repo "github/octocat" changed owner
```
