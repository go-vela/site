---
title: "View"
linkTitle: "View"
weight: 15
description: >
  Learn how to view a secret.
---

## Information

```sh
NAME:
   vela view secret - View details of the provided secret

USAGE:
   vela view secret [command options] [arguments...]

DESCRIPTION:
   Use this command to view a secret.
```

## Flags

```sh
OPTIONS:
   --engine value            Provide the engine for where the secret to be stored (default: "native") [$VELA_SECRET_ENGINE, $SECRET_ENGINE]
   --type value              Provide the kind of secret to be stored (default: "repo") [$SECRET_TYPE]
   --org value               Provide the organization for the repository [$SECRET_ORG]
   --repo value              Provide the repository contained with the organization [$SECRET_REPO]
   --team value              Provide the team contained with the organization [$SECRET_TEAM]
   --name value              Provide the name of the secret [$SECRET_NAME]
   --output value, -o value  Print the output in json format
```

## Examples

```sh
EXAMPLES:
 1. View repository secret details.
    $ vela view secret --engine native --type repo --org github --repo octocat --name foo
 2. View organization secret details.
    $ vela view secret --engine native --type org --org github --repo '*' --name foo
 3. View shared secret details.
    $ vela view secret --engine native --type shared --org github --team octokitties --name foo
 4. View secret details for a repository with json output.
    $ vela view secret --engine native --type repo --org github --repo octocat --name foo --output json
 5. View secret details with default native engine or when engine and type environment variables are set.
    $ vela view secret --org github --repo octocat --name foo
```

## Sample

```sh
$ vela view secret --engine native --type repo --org github --repo octocat --name foo

id: 1
org: github
repo: octocat
team: ""
name: foo
value: ""
type: repo
images: null
events:
  - push
  - pull_request
```
