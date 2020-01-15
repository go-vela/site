---
title: "Update"
linkTitle: "Update"
weight: 10
description: >
  Learn how to update a config.
---

## Information

```sh
NAME:
   vela update config - Update a config file

USAGE:
   vela update config [command options] [arguments...]

DESCRIPTION:
   Use this command to update a config file.
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
 1. Update CLI config with address.
    $ vela update config --addr https://vela-server.localhost
 2. Update CLI config with personal token.
    $ vela update config --token fakeToken
 3. Update CLI config with specific API version.
    $ vela update config --api-version v1
 4. Update CLI config with debug log level.
    $ vela update config --log-level debug
```

## Sample

```sh
$ vela update config --org github

addr: https://vela-server.localhost
token: qwerty123
api-version: v1
log-level: info
org: github
```
