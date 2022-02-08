---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list secrets.
---

## Command

```
$ vela get secret <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get secret --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name            | Description                            | Environment Variables          |
| --------------- | -------------------------------------- | ------------------------------ |
| `org`           | name of organization for the secrets   | `VELA_ORG`, `SECRET_ORG`       |
| `repo`          | name of repository for the secrets     | `VELA_REPO`, `SECRET_REPO`     |
| `secret.engine` | name of engine that stores the secrets | `VELA_ENGINE`. `SECRET_ENGINE` |
| `secret.type`   | name of type of secrets being stored   | `VELA_TYPE`, `SECRET_TYPE`     |
| `team`          | name of team for the secrets           | `VELA_TEAM`, `SECRET_TEAM`     |
| `output`        | format the output for the secrets      | `VELA_OUTPUT`, `SECRET_OUTPUT` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `secret.engine`
- `secret.type`
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
$ vela get secret --secret.engine native --secret.type repo 
```

#### Targeted Request

```sh
$ vela get secret --secret.engine native --secret.type repo --org github --repo octocat
```

#### Response

```sh
NAME  ORG             TYPE  EVENTS
foo   github/octocat  repo  push,pull_request
```
