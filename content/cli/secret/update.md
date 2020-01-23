---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a secret.
---

## Command

```
$ vela update secret <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update secret --help`.
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
This command also supports setting the `engine`, `type`, `org` or `repo` parameters via a configuration file.

For more information, please review the [CLI config documentation](/docs/cli/config).
{{% /alert %}}

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/cli/install).

To setup the CLI, please review the [authentication documentation](/docs/cli/authentication).
{{% /alert %}}

#### Request

```sh
vela update secret --engine native --type repo --org github --repo octocat --name foo --value baz
```

#### Response

```sh
secret "foo" was updated
```

## Advanced

#### Input From File

Vela supports updating a single-line or multi-line secret from a file using the `@` symbol.

```sh
# Syntax
vela update secret --engine native --type repo --org github --repo octocat --name foo --value @/path/to/file

# Example
vela update secret --engine native --type repo --org github --repo octocat --name foo --value @$HOME/tmp/secret.txt
```

#### Secrets From File

Vela supports updating multiple secrets from a file using the `filename` parameter.

```sh
vela update secret -f secret.yml
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
