---
title: "Authentication"
weight: 10
description: >
  Learn how authenticating with the Vela CLI works.
---

## Overview

Authentication with the Vela CLI is the responsibility of the client initiating the request.

Each request requires a server address. You can provide this variable to the CLI in three ways:

- Configuration File
- Environment Variable
- Flag

{{% alert color="info" %}}
A configuration file is the recommended method for providing the API address to the CLI.
{{% /alert %}}

### Configuration File

{{% alert color="info" %}}
The default path for this configuration file can be found @ `$HOME/.vela/config.yml`.
{{% /alert %}}

Log in:

```sh
# Syntax
vela login --api.addr <vela server url>

# Example
vela login --api.addr https://vela-server.localhost
```

Confirm authentication via browser prompt:

```
Open https://vela-server.localhost in your browser and complete authentication (Press Enter to confirm):
```

Confirm to generate or update the configuration file prompt:

```
Authentication complete. Continue to save configuration (existing config will be overwritten):
```

{{% alert color="info" %}}
For more information, you can visit the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

### Environment Variables

Configure the environment with the `VELA_ADDR` environment variable:

```sh
export VELA_ADDR=https://vela-server.localhost
```

Log in and confirm the two prompts as stated above:

```sh
vela login
```

{{% alert color="info" %}}
It's recommended to add these to your terminal profile (`~/.bashrc` or `~/.zshrc`)
{{% /alert %}}

### Flags

Log in and confirm the two prompts as stated above:

```sh
# Syntax
vela --api.addr <vela server url> login

# Example
vela --api.addr https://vela-server.localhost login
```
