---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list logs for a build.
---

## Command

```
$ vela get log <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get log --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                      | Environment Variables       |
| -------- | -------------------------------- | --------------------------- |
| `org`    | name of organization for the log | `VELA_ORG`, `LOG_ORG`       |
| `repo`   | name of repository for the log   | `VELA_REPO`, `LOG_REPO`     |
| `build`  | number of the build for the log  | `VELA_BUILD`, `LOG_BUILD`   |
| `output` | format the output for the logs   | `VELA_OUTPUT`, `LOG_OUTPUT` |

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
$ vela get log --org github --repo octocat --build 5
```

#### Response

```sh
$ git init
Initialized empty Git repository in /home/github_octocat_5/.git/
$ git remote add origin https://github.com/github/octocat.git
$ git remote --verbose
origin  https://github.com/github/octocat.git (fetch)
origin  https://github.com/github/octocat.git (push)
$ git fetch --no-tags origin refs/heads/master
From https://github.com/github/octocat
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
$ git reset --hard afafce5e33a8efd4340613b31a953107d6dec3a3
HEAD is now at afafce5 Dummy commit

$ echo "Hello World!"
Hello World!
```
