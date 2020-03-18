---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect logs.
---

## Command

```
$ vela view log <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view log --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name    | Description          | Environment    |
| ------- | -------------------- | -------------- |
| `org`   | name of organization | `BUILD_ORG`    |
| `repo`  | name of repository   | `BUILD_REPO`   |
| `build` | number of build      | `BUILD_NUMBER` |

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

To setup the CLI, please review the [authentication documentation](/docs/cli/authentication).
{{% /alert %}}

#### Request

```sh
$ vela view log --org github --repo octocat --build 5
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
