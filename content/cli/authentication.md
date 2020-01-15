---
title: "Authentication"
weight: 10
description: >
  Learn how to authenticate with the CLI.
---

To authenticate with Vela, users need to provide the server address and personal token. There are three ways to provide the address and token to the CLI:

- Configuration File **(recommended)**
- Environment Variables
- Flags

### Configuration File

Log in and capture the personal token:

```sh
# Syntax
vela --addr <vela server url> login

# Example
vela --addr https://vela-server.localhost login
```

Generate the configuration file:

```sh
# Syntax
vela generate config --addr <vela server url> --token <personal token>

# Example
vela generate config --addr https://vela-server.localhost --token qwerty123
```

The default path for this configuration file can be found @ `~/.vela/config.yml`.

_To see the file config file reference see the [config section](/vela/doc-site/reference/cli/config)._

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

It is recommended to add these to the terminal profile (`~/.bashrc` or `~/.zshrc`)

### Flags

Log in and capture the personal token:

```sh
# Syntax
vela --addr <vela server url> login

# Example
vela --addr https://vela-server.localhost login
```

Pass the personal token as a flag argument:

```sh
# Syntax
vela --addr <vela server url> --token <personal token>

# Example
vela --addr https://vela-server.localhost --token qwerty123
```
