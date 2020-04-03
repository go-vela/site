---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a secret.
---

## Command

```
$ vela add secret <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela add secret --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                       | Environment     |
| ---------- | --------------------------------- | --------------- |
| `engine`   | name of engine                    | `SECRET_ENGINE` |
| `type`     | name of type of secret            | `SECRET_TYPE`   |
| `org`      | name of organization              | `SECRET_ORG`    |
| `repo`     | name of repository                | `SECRET_REPO`   |
| `team`     | name of team                      | `SECRET_TEAM`   |
| `name`     | name of secret                    | `SECRET_NAME`   |
| `value`    | value of secret                   | `SECRET_VALUE`  |
| `image`    | limit secret to specific image(s) | `SECRET_IMAGES` |
| `event`    | limit secret to specific event(s) | `SECRET_EVENTS` |
| `filename` | add secret(s) from a file         | `N/A`           |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `engine`
- `type`
- `org`
- `repo`

For more information, please review the [CLI config documentation](/docs/cli/config/).
{{% /alert %}}

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/cli/authentication/).
{{% /alert %}}

#### Request

```sh
vela add secret --engine native --type repo --org github --repo octocat --name foo --value bar
```

#### Response

```sh
secret "foo" was added
```

## Advanced

#### Organization Level Secrets

Vela supports secrets at an organization level, which allows all repositories in that org to have access to a single secret. When creating `--type org` secrets the `--repo` flag is still required and allows for a wildcard.

```
vela add secret --engine native --type org --repo '*' --name foo --value bar
```

#### Input From File

Vela supports creating a single-line or multi-line secret from a file using the `@` symbol.

```sh
# Syntax
vela add secret --engine native --type repo --org github --repo octocat --name foo --value @/path/to/file

# Example
vela add secret --engine native --type repo --org github --repo octocat --name foo --value @$HOME/tmp/secret.txt
```

#### Secrets From File

Vela supports creating multiple secrets from a file using the `filename` parameter.

```sh
vela add secret -f secret.yml
```

##### Single YAML document

```yaml
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

##### Multiple YAML document

```yaml
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
