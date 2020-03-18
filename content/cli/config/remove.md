---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a config.
---

## Command

```
$ vela remove config <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela remove config --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name            | Description                  | Environment |
| --------------- | ---------------------------- | ----------- |
| `addr`          | URL to server                | `N/A`       |
| `token`         | user token from server       | `N/A`       |
| `api-version`   | API version for server       | `N/A`       |
| `log-level`     | change the CLI logging level | `N/A`       |
| `org`           | name of organization         | `N/A`       |
| `repo`          | name of repository           | `N/A`       |
| `secret-engine` | name of secret backend       | `N/A`       |
| `secret-type`   | name of secret type          | `N/A`       |

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
vela remove config
```

#### Response
