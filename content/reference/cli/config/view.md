---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a config.
---

## Command

```
$ vela view config <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view config --help`.
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
vela view config
```

#### Response

```sh
api:
  addr: https://vela.example.com
  access_token: superSecretAccessToken
  refresh_token: superSecretRefreshToken
  version: v1
log:
  level: info
no-git: "false"
secret: {}
```
