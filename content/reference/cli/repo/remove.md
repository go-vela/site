---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a repo.
---

## Command

```
$ vela remove repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela remove repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                             | Environment Variables        |
| -------- | --------------------------------------- | ---------------------------- |
| `org`    | name of organization for the repository | `VELA_ORG`, `REPO_ORG`       |
| `repo`   | name of repository                      | `VELA_REPO`, `REPO_NAME`     |
| `output` | format the output for the repository    | `VELA_OUTPUT`, `REPO_OUTPUT` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`
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
vela remove repo --org github --repo octocat
```

#### Response

```sh
repo "github/octocat" was deleted
```
