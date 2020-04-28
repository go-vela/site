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

| Name     | Description            | Environment     |
| -------- | ---------------------- | --------------- |
| `engine` | name of engine         | `SECRET_ENGINE` |
| `type`   | name of type of secret | `SECRET_TYPE`   |
| `org`    | name of organization   | `SECRET_ORG`    |
| `repo`   | name of repository     | `SECRET_REPO`   |
| `team`   | name of team           | `SECRET_TEAM`   |
| `output` | format the output      | `N/A`           |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `engine`
- `type`
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
vela get secret --engine native --type repo --org github --repo octocat
```

#### Response

```sh
NAME  ORG             TYPE  EVENTS
foo   github/octocat  repo  push,pull_request
```
