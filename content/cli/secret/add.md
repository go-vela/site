---
title: "Add"
linkTitle: "Add"
weight: 5
description: >
  Learn how to add a secret.
---

## Information

```sh
NAME:
   vela add secret - Add a secret

USAGE:
   vela add secret [command options] [arguments...]

DESCRIPTION:
   Use this command to add a secret.
```

## Flags

```sh
OPTIONS:
   --engine value              Provide the engine for where the secret to be stored (default: "native") [$SECRET_ENGINE]
   --type value                Provide the kind of secret to be stored (default: "repo") [$SECRET_TYPE]
   --org value                 Provide the organization for the repository [$SECRET_ORG]
   --repo value                Provide the repository contained with the organization [$SECRET_REPO]
   --team value                Provide the team contained with the organization [$SECRET_TEAM]
   --name value                Provide the name of the secret [$SECRET_NAME]
   --value value               Provide the value of the secret [$SECRET_VALUE]
   --image value               Secret limited to these images [$SECRET_IMAGES]
   --event value               Secret limited to these events (default: "push") [$SECRET_EVENTS]
   --filename value, -f value  Filename to use to add the secret or secrets
```

## Examples

```sh
EXAMPLES:
 1. Add a secret for a repository with push events.
    $ vela add secret --engine native --type repo --org github --repo octocat --name foo --value bar
 2. Add a secret for a org with push events.
    $ vela add secret --engine native --type org --org github --repo '*' --name foo --value bar
 3. Add a shared secret for the platform
    $ vela add secret --engine native --type shared --org github --team octokitties --name foo --value bar
 4. Add a secret for a repository with all event types enabled.
    $ vela add secret --engine native --type repo --org github --repo octocat --name foo --value bar --event push --event pull_request --event tag --event deployment
 5. Add a secret from a file.
    $ vela add secret --engine native --type repo --org github --repo octocat --name foo --value @/path/to/file
 6. Add a native repo secret with an image whitelist.
    $ vela add secret --engine native --type repo --org github --repo octocat --name foo --value bar --image alpine --image golang
 7. Add a repo secret with default native engine or when engine and type environment variables are set.
  $ vela add secret --org github --repo octocat --name foo --value bar
 8. Add a secret or secrets from a file
    $ vela add secret -f secret.yml
```

## Sample

```sh
$ vela add secret --engine native --type repo --event push --event pull_request --org github --repo octocat --name foo --value bar

secret "foo" was addd
```

## Secrets from a File

Vela supports creating a single-line or multi-line secret saved in a file.

#### Examples
_Example CLI command for repo secret type_
```sh
$ vela add secret --engine native --type repo --org github --repo octocat --name foo --value @/path/to/file

$ vela add secret --engine native --type repo --org github --repo octocat --name foo --value @$HOME/some_directory/secret_file_bar.txt
```

_Example CLI command for org secret type_
```sh
$ vela add secret --engine native --type org --org github --repo '*' --name foo --value @/path/to/file

$ vela add secret --engine native --type org --org github --repo '*' --name foo --value @$HOME/some_directory/secret_file_bar.txt
```

_Example CLI command for shared secret type_
```sh
$ vela add secret --engine native --type shared --org github --team foobar --name foo --value @/path/to/file

$ vela add secret --engine native --type shared --org github --team foobar --name foo --value @$HOME/some_directory/secret_file_bar.txt
```

##### Advanced

_Example CLI command for repo secret type_
```sh
$ vela add secret -f secret.yml
```

_Example secret.yml file for above command_
```yaml
# Option 1
---
metadata:
  api_version: v1
  engine: native
secrets:
  - org: octocat
    repo: github
    name: foo
    value: bar
    type: repo
    images:
      - golang:latest
    events:
      - push
      - pull_request
  - org: github
    team: octokitties
    name: foo1
    value: "@/path/to/file/bar1"
    type: shared
    images:
      - golang:latest
    events:
      - push
      - pull_request
```

```yaml
# Option 2
---
metadata:
  api_version: v1
  engine: native
secrets:
  - org: github
    repo: octocat
    name: foo
    value: bar
    type: repo
    images:
      - golang:latest
    events:
      - push
      - pull_request
---
metadata:
  api_version: v1
  engine: vault
secrets:
  - org: git
    team: octokitties
    name: foo1
    value: "@/path/to/file/bar1"
    type: shared
    images:
      - golang:latest
    events:
      - push
      - pull_request
```
