---
title: "Generate"
linkTitle: "Generate"
description: >
  Learn how to produce a config.
---

## Command

```
$ vela generate config <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela generate config --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name            | Description                         | Environment Variables                    |
| --------------- | ----------------------------------- | ---------------------------------------- |
| `api.addr`      | full URL to API server              | `VELA_ADDR`, `CONFIG_ADDR`               |
| `api.token`     | user token from API server          | `VELA_TOKEN`, `CONFIG_TOKEN`             |
| `api.version`   | version of API for server           | `VELA_API_VERSION`, `CONFIG_API_VERSION` |
| `log.level`     | set the level of logging            | `VELA_LOG_LEVEL`, `CONFIG_LOG_LEVEL`     |
| `output`        | format the output for API results   | `VELA_OUTPUT`, `CONFIG_OUTPUT`           |
| `org`           | name of organization for API calls  | `VELA_ORG`, `CONFIG_ORG`                 |
| `repo`          | name of repository for API calls    | `VELA_REPO`, `CONFIG_REPO`               |
| `secret.engine` | name of secret engine for API calls | `VELA_ENGINE`, `CONFIG_ENGINE`           |
| `secret.type`   | name of secret type for API calls   | `VELA_TYPE`, `CONFIG_TYPE`               |

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
vela generate config --api.addr https://vela-server.localhost --api.token superSecretToken
```

#### Response

```sh
api:
  addr: https://vela-server.localhost
  token: superSecretToken
  version: "1"
log:
  level: info
```
