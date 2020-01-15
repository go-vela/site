---
title: "Config"
weight: 5
description: >
  Learn how to generate a config file.
---

## Information

```sh
NAME:
   vela generate config - Generate a config yaml in a directory

USAGE:
   vela generate config [command options] [arguments...]

DESCRIPTION:
   Use this command to add a config file.
```

## Flags

```sh
OPTIONS:
   --addr value           location of vela server
   --token value          User token for Vela server
   --api-version value    api version to use for Vela server
   --log-level value      set log level - options: (trace|debug|info|warn|error|fatal|panic)
   --org value            Provide the organization for the repository
   --repo value           Provide the repository contained within the organization
   --secret-engine value  Provide the engine for where the secret to be stored
   --secret-type value    Provide the kind of secret to be stored
```

## Examples

```sh
EXAMPLES:
 1. Generate CLI config from environment.
    $ vela generate config
 2. Generate CLI config with address and token.
    $ vela generate config --addr https://vela-server.localhost --token fakeToken
 3. Generate CLI config with specific API version.
    $ vela generate config --api-version v1
 4. Generate CLI config with debug log level.
    $ vela generate config --log-level debug
```

## Sample

```sh
$ vela generate config --addr https://vela-server.localhost --token qwerty123

addr: https://vela-server.localhost
token: qwerty123
api-version: v1
log-level: info
```
