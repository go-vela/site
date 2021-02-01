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

{{% alert color="warning" %}}
Providing no parameters to this command will remove the entire configuration file.
{{% /alert %}}

| Name                | Description                         | Environment Variables                        |
| ------------------- | ----------------------------------- | -------------------------------------------- |
| `api.addr`          | removes the API address field       | `VELA_ADDR`, `CONFIG_ADDR`                   |
| `api.token.access`  | removes the API access token field  | `VELA_ACCESS_TOKEN`, `CONFIG_ACCESS_TOKEN`   |
| `api.token.refresh` | removes the API refresh token field | `VELA_REFRESH_TOKEN`, `CONFIG_REFRESH_TOKEN` |
| `api.token`         | removes the API token field         | `VELA_TOKEN`, `CONFIG_TOKEN`                 |
| `api.version`       | removes the API version field       | `VELA_API_VERSION`, `CONFIG_API_VERSION`     |
| `log.level`         | removes the log level field         | `VELA_LOG_LEVEL`, `CONFIG_LOG_LEVEL`         |
| `output`            | removes the output field            | `VELA_OUTPUT`, `CONFIG_OUTPUT`               |
| `org`               | removes the org field               | `VELA_ORG`, `CONFIG_ORG`                     |
| `repo`              | removes the repo field              | `VELA_REPO`, `CONFIG_REPO`                   |
| `secret.engine`     | removes the secret engine field     | `VELA_ENGINE`, `CONFIG_ENGINE`               |
| `secret.type`       | removes the secret type field       | `VELA_TYPE`, `CONFIG_TYPE`                   |

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/li/authentication/).
{{% /alert %}}

#### Request

```sh
vela remove config
```

#### Response
