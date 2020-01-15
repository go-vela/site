---
title: "Remove"
linkTitle: "Remove"
weight: 25
description: >
  Learn how to remove a secret.
---

## Information

```sh
NAME:
   vela remove secret - Remove a secret

USAGE:
   vela remove secret [command options] [arguments...]

DESCRIPTION:
   Use this command to remove a secret.
```

## Flags

```sh
OPTIONS:
   --engine value  Provide the engine for where the secret to be stored (default: "native") [$VELA_SECRET_ENGINE, $SECRET_ENGINE]
   --type value    Provide the kind of secret to be stored (default: "repo") [$SECRET_TYPE]
   --org value     Provide the organization for the repository [$SECRET_ORG]
   --repo value    Provide the repository contained with the organization [$SECRET_REPO]
   --team value    Provide the team contained with the organization [$SECRET_TEAM]
   --name value    Provide the name of the secret [$SECRET_NAME]
```

## Examples

```sh
EXAMPLES:
 1. Remove a secret for a repository.
    $ vela remove secret --engine native --type repo --org github --repo octocat --name foo
 2. Remove a secret for a org.
    $ vela remove secret --engine native --type org --org github --repo '*' --name foo
 3. Remove a shared secret for the platform.
    $ vela remove secret --engine native --type shared --org github --team octokitties --name foo
 4. Remove a repo secret with default native engine or when engine and type environment variables are set.
    $ vela remove secret --org github --repo octocat --name foo
```

## Sample

```sh
$ vela delete repo --org github --repo octocat

secret "foo" was deleted
```
