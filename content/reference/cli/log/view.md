---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect logs for a build, step, or service.
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

| Name      | Description                       | Environment Variables         |
| --------- | --------------------------------- | ----------------------------- |
| `org`     | name of organization for the log  | `VELA_ORG`, `LOG_ORG`         |
| `repo`    | name of repository for the log    | `VELA_REPO`, `LOG_REPO`       |
| `build`   | number of the build for the log   | `VELA_BUILD`, `LOG_BUILD`     |
| `service` | number of the service for the log | `VELA_SERVICE`, `LOG_SERVICE` |
| `step`    | number of the step for the log    | `VELA_STEP`, `LOG_STEP`       |
| `output`  | format the output for the logs    | `VELA_OUTPUT`, `LOG_OUTPUT`   |

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
$ pwd
~/github/octocat
$ vela view log --build 5 --step 1
```

#### Targeted Request

```sh
$ vela view log --org github --repo octocat --build 5 --step 1
```

#### Response

```sh
$ git init
Initialized empty Git repository in /vela/src/github.com/github/octocat/.git/
$ git remote add origin https://github.com/github/octocat.git
$ git remote --verbose
origin  https://github.com/github/octocat.git (fetch)
origin  https://github.com/github/octocat.git (push)
$ git fetch --no-tags origin refs/heads/main
From https://github.com/github/octocat
 * branch            main     -> FETCH_HEAD
 * [new branch]      main     -> origin/main
$ git reset --hard afafce5e33a8efd4340613b31a953107d6dec3a3
HEAD is now at afafce5 Dummy commit
```
