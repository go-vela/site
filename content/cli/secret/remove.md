---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a secret.
---

## Command

```
$ vela remove secret <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela remove secret --help`.
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
| `name`   | name of secret         | `SECRET_NAME`   |

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

To setup the CLI, please review the [authentication documentation](/docs/cli/authentication).
{{% /alert %}}

#### Request

```sh
vela remove secret --engine native --type repo --org github --repo octocat --name foo
```

#### Response

```sh
secret "foo" was deleted
```
