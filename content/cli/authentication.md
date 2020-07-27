---
title: "Authentication"
weight: 10
description: >
  Learn how authenticating with the Vela CLI works.
---

## Overview

Authentication with the Vela CLI is the responsibility of the client initiating the request.

Each request requires a server address and user token to be provided. You can provide these variables to the CLI in three ways:

- Configuration File
- Environment Variables
- Flags

{{% alert color="info" %}}
A configuration file is the recommended method for providing the API address and token to the CLI.
{{% /alert %}}

### Configuration File

{{% alert color="info" %}}
The default path for this configuration file can be found @ `$HOME/.vela/config.yml`.
{{% /alert %}}

Log in and capture the personal token:

```sh
# Syntax
vela login --api.addr <vela server url>

# Example
vela login --api.addr https://vela-server.localhost
```

Generate the configuration file:

```sh
# Syntax
vela generate config --api.addr <vela server url> --api.token <personal token>

# Example
vela generate config --api.addr https://vela-server.localhost --api.token qwerty123
```

{{% alert color="info" %}}
For more information, you can visit the [CLI config documentation](/docs/cli/config/).
{{% /alert %}}

### Environment Variables

Configure the environment with the `VELA_ADDR` environment variable:

```sh
export VELA_ADDR=https://vela-server.localhost
```

Log in and capture the personal token:

```sh
vela login
```

Configure the environment with the `VELA_TOKEN` environment variable:

```sh
export VELA_TOKEN=<personal token>
```

{{% alert color="info" %}}
It's recommended to add these to your terminal profile (`~/.bashrc` or `~/.zshrc`)
{{% /alert %}}

### Flags

Log in and capture the personal token:

```sh
# Syntax
vela --api.addr <vela server url> login

# Example
vela --api.addr https://vela-server.localhost login
```

Pass the personal token as a flag argument:

```sh
# Syntax
vela --api.addr <vela server url> --api.token <personal token>

# Example
vela --api.addr https://vela-server.localhost --api.token qwerty123
```
