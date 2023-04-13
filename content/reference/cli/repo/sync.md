---
title: "Sync"
linkTitle: "Sync"
description: >
  Learn how to sync repos in database with GitHub.
---

## Command

```
$ vela sync repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela sync repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                             | Environment Variables        |
| -------- | --------------------------------------- | ---------------------------- |
| `org`    | name of organization for the repository | `VELA_ORG`, `REPO_ORG`       |
| `repo`   | name of repository                      | `VELA_REPO`, `REPO_NAME`     |
| `all`    | bool flag to sync all repos in an org   | `VELA_SYNC_ALL`, `SYNC_ALL`  |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

## Description

The sync command allows users to re-align their repository in Vela with its SCM mirror. This discrepancy can come in the form of a repository that has been deleted from the SCM but not in Vela. 

Further, as of `v0.19.0`, the sync command can be used to adjust events that are sent to Vela from the SCM that the Vela-instance of the repo is not subscribed to. For example, if your audit page has errors like

```sh
"unable to process webhook: <org>/<repo> does not have comment events enabled"
```

running the sync command should re-configure the SCM webhook to only send events that are allowed. Once aligned, you should not have to run this command again, even if the subscribed events are changed.

## Samples

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
$ pwd
~/github/octocat
$ vela sync repo
```

#### Targeted Request

```sh
$ vela sync repo --org github --repo octocat
```

#### Response

```sh
repo "github/octocat" synced
```

#### Request

```sh
$ pwd
~/github/octocat
$ vela sync repo --all
```

#### Targeted Request

```sh
$ vela sync repo --org github --all
```

#### Response

```sh
org "github" synced