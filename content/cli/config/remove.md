---
title: "Remove"
linkTitle: "Remove"
weight: 15
description: >
  Learn how to remove a config.
---

## Information

```sh
NAME:
   vela remove config - Remove a field or all fields in the config file.

USAGE:
   vela remove config [command options] [arguments...]

DESCRIPTION:
   Use this command to remove a field or all fields in the config file.
```

## Flags

```sh
OPTIONS:
   --addr           removes the addr field from the config
   --token          removes the token field from the config
   --api-version    removes the api-version field from the config
   --log-level      removes the log-level field from the config
   --org            removes the org field from the config
   --repo           removes the repo field from the config
   --secret-engine  removes the secret-engine field from the config
   --secret-type    removes the secret-type field from the config
```

## Examples

```sh
EXAMPLES:
 1. Remove the CLI config file.
    $ vela remove config
 2. Remove the address from the CLI config file.
    $ vela remove config --address
 3. Remove the API version from the CLI config file.
    $ vela remove config --api-version
 4. Remove the log level from the CLI config file.
    $ vela remove config --log-level
```

## Sample

```sh
$ vela remove config
```
