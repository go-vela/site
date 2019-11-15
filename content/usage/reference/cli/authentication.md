---
title: "Authentication"
weight: 10
description: >
  Learn how to authenticate with the CLI.
---

To authenticate with Vela, users need to provide the server address and personal token. There are three ways to provide the address and token to the CLI:

* Configuration File **(recommended)**
* Environment Variables
* Flags

### Configuration File

Log in and capture the personal token:

```sh
vela --addr https://vela-api.company.com login
```

Generate the configuration file:

```sh
vela generate config --addr https://vela-api.company.com --token <personal token>
```

The default path for this configuration file can be found @ `~/.vela/config.yml`.

_To see the file config file reference see the [config section](/vela/doc-site/reference/cli/config)._

### Environment Variables

Configure the environment with the `VELA_ADDR` environment variable:

```sh
export VELA_ADDR=https://vela-api.company.com
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
vela --addr https://vela-api.company.com login
```

Pass the personal token as a flag argument:

```sh
vela --addr https://vela-api.company.com --token <personal token> ...
```
