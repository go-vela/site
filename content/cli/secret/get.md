---
title: "Get"
linkTitle: "Get"
weight: 10
description: >
  Learn how to get a secret.
---

## Information

```sh
NAME:
   vela get secret - Display a list of secrets

USAGE:
   vela get secret [command options] [arguments...]

DESCRIPTION:
   Use this command to get a list of secrets.
```

## Flags

```sh
OPTIONS:
   --engine value            Provide the engine for where the secret to be stored (default: "native") [$VELA_SECRET_ENGINE, $SECRET_ENGINE]
   --type value              Provide the kind of secret to be stored (default: "repo") [$SECRET_TYPE]
   --org value               Provide the organization for the repository [$SECRET_ORG]
   --repo value              Provide the repository contained with the organization [$SECRET_REPO]
   --team value              Provide the team contained with the organization [$SECRET_TEAM]
   --output value, -o value  Print the output in a yaml or json format
```

## Examples

```sh
EXAMPLES:
 1. Get repository secrets.
    $ vela get secret --engine native --type repo --org github --repo octocat
 2. Get organization secrets.
    $ vela get secret --engine native --type org --org github --repo '*'
 3. Get shared secrets.
    $ vela get secret --engine native --type shared --org github --team octokitties
 4. Get secrets for a repository with wide view output.
    $ vela get secret --output wide --engine native --type repo --org github --repo octocat
 5. Get secrets for a repository with yaml output.
    $ vela get secret --output yaml --engine native --type repo --org github --repo octocat
 6. Get secrets for a repository with json output.
    $ vela get secret --output json --engine native --type repo --org github --repo octocat
 7. Get repository secrets with default native engine or when engine and type environment variables are set.
    $ vela get secret --org github --repo octocat
```

## Sample

```sh
$ vela get secret --engine native --type repo --org github --repo octocat

NAME  ORG             TYPE  EVENTS
foo   github/octocat  repo  push,pull_request
```
