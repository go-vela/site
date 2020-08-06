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

| Name       | Description                               | Environment Variables            |
| ---------- | ----------------------------------------- | -------------------------------- |
| `org`      | name of organization for the repository   | `VELA_ORG`, `REPO_ORG`           |
| `repo`     | name of repository                        | `VELA_REPO`, `REPO_NAME`         |
| `output`   | format the output for the repository      | `VELA_OUTPUT`, `REPO_OUTPUT`     |
| `page`     | prints a specific page of repositories    | `VELA_PAGE`, `REPO_PAGE`         |
| `per.page` | number of repositories to print per page  | `VELA_PER_PAGE`, `REPO_PER_PAGE` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`
- `output`

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
vela get repo
```

#### Response

```sh
ORG/REPO        STATUS  EVENTS             VISIBILITY  BRANCH
github/octocat  true    push,pull_request  public      master
```
