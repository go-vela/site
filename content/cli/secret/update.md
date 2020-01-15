---
title: "Update"
linkTitle: "Update"
weight: 20
description: >
  Learn how to update a secret.
---

## Information

```sh
NAME:
   vela update secret - Update a secret

USAGE:
   vela update secret [command options] [arguments...]

DESCRIPTION:
   Use this command to update a secret.
```

## Flags

```sh
OPTIONS:
   --engine value              Provide the engine for where the secret to be stored (default: "native") [$VELA_SECRET_ENGINE, $SECRET_ENGINE]
   --type value                Provide the kind of secret to be stored (default: "repo") [$SECRET_TYPE]
   --org value                 Provide the organization for the repository [$SECRET_ORG]
   --repo value                Provide the repository contained with the organization [$SECRET_REPO]
   --team value                Provide the team contained with the organization [$SECRET_TEAM]
   --name value                Provide the name of the secret [$SECRET_NAME]
   --value value               Provide the value of the secret [$SECRET_VALUE]
   --image value               Secret limited to these images [$SECRET_IMAGES]
   --event value               Secret limited to these events [$SECRET_EVENTS]
   --filename value, -f value  Filename to use to create the secret or secrets
```

## Examples

```sh
EXAMPLES:
 1. Update a secret value for a repository.
    $ vela update secret --engine native --type repo --org github --repo octocat --name foo --value bar
 2. Update a secret value for a org.
    $ vela update secret --engine native --type org --org github --repo '*' --name foo --value bar
 3. Update a shared secret value for the platform.
    $ vela update secret --engine native --type shared --team octokitties --name foo --value bar
 4. Update a secret for a repository with all event types enabled.
    $ vela update secret --engine native --type repo --org github --repo octocat --name foo --event push --event pull_request --event tag --event deployment
 5. Update a secret from a file.
    $ vela update secret --engine native --type repo --org github --repo octocat --name foo --value @/path/to/file
 6. Update a secret for a repository with an image whitelist.
    $ vela update secret --engine native --type repo --org github --repo octocat --name foo --image alpine --image golang
 7. Update a repo secret value with default native engine or when engine and type environment variables are set.
  $ vela update secret --org github --repo octocat --name foo --value bars
 8. Update with data from a secret file.
  $ vela update secret -f secret.yml
```

## Sample

```sh
$ vela update repo --org github --repo octocat --event push --event pull_request --event deployment --name foo

secret "foo" was updated
```

## Secrets from a File

Vela supports updating a single-line or multi-line secret saved in a file.

#### Examples
_Example CLI command for repo secret type_
```sh
$ vela update secret --engine native --type repo --org github --repo octocat --name foo --value @/path/to/file

$ vela update secret --engine native --type repo --org github --repo octocat --name foo --value @$HOME/some_directory/secret_file_bar.txt
```

_Example CLI command for org secret type_
```sh
$ vela update secret --engine native --type org --org github --repo '*' --name foo --value @/path/to/file

$ vela update secret --engine native --type org --org github --repo '*' --name foo --value @$HOME/some_directory/secret_file_bar.txt
```

_Example CLI command for shared secret type_
```sh
$ vela update secret --engine native --type shared --org github --team foobar --name foo --value @/path/to/file

$ vela update secret --engine native --type shared --org github --team foobar --name foo --value @$HOME/some_directory/secret_file_bar.txt
```
