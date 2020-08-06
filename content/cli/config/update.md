---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a config.
---

## Command

```
$ vela update config <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update config --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name            | Description                     | Environment Variables                    |
| --------------- | ------------------------------- | ---------------------------------------- |
| `api.addr`      | updates the API address field   | `VELA_ADDR`, `CONFIG_ADDR`               |
| `api.token`     | updates the API token field     | `VELA_TOKEN`, `CONFIG_TOKEN`             |
| `api.version`   | updates the API version field   | `VELA_API_VERSION`, `CONFIG_API_VERSION` |
| `log.level`     | updates the log level field     | `VELA_LOG_LEVEL`, `CONFIG_LOG_LEVEL`     |
| `output`        | updates the output field        | `VELA_OUTPUT`, `CONFIG_OUTPUT`           |
| `org`           | updates the org field           | `VELA_ORG`, `CONFIG_ORG`                 |
| `repo`          | updates the repo field          | `VELA_REPO`, `CONFIG_REPO`               |
| `secret.engine` | updates the secret engine field | `VELA_ENGINE`, `CONFIG_ENGINE`           |
| `secret.type`   | updates the secret type field   | `VELA_TYPE`, `CONFIG_TYPE`               |

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
vela update config --org github
```

#### Response

```sh
api:
  addr: https://vela-server.localhost
  token: superSecretToken
  version: "1"
log:
  level: info
org: github
```
