---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify platform settings.
---

## Command

```
$ vela update settings <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update settings --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name                           | Description                                             | Environment Variables                |
| ------------------------------ | ------------------------------------------------------- | ------------------------------------ |
| `compiler.clone-image`         | image used by the compiler to clone repositories        | `VELA_COMPILER_CLONE_IMAGE`          |
| `compiler.template-depth`      | maximum depth of nested templates                       | `VELA_COMPILER_TEMPLATE_DEPTH`       |
| `compiler.starlark-exec-limit` | maximum execution limit for Starlark templates          | `VELA_COMPILER_STARLARK_EXEC_LIMIT`  |
| `queue.add-route`              | add a route to the queue                                | `VELA_QUEUE_ADD_ROUTES`              |
| `queue.drop-route`             | drop a route from the queue                             | `VELA_QUEUE_DROP_ROUTES`             |
| `add-repo`                     | name of repository to add to the global allowlist       | `VELA_REPO_ALLOWLIST_ADD_REPOS`      |
| `drop-repo`                    | name of repository to drop from the global allowlist    | `VELA_REPO_ALLOWLIST_DROP_REPOS`     |
| `add-schedule`                 | name of repository to add to the schedules allowlist    | `VELA_SCHEDULE_ALLOWLIST_ADD_REPOS`  |
| `drop-schedule`                | name of repository to drop from the schedules allowlist | `VELA_SCHEDULE_ALLOWLIST_DROP_REPOS` |
| `file`                         | path to a json/yaml file containing settings updates    | `VELA_FILE`                          |

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
$ pwd
~/github/octocat
$ vela update settings --secret.engine native
```

#### Targeted Request

```sh
$ vela update settings --secret.engine native
```

#### Response

```yaml
id: 1
compiler:
    clone_image: target/vela-git:latest
    template_depth: 3
    starlark_exec_limit: 7500
queue:
    routes:
        - vela
repo_allowlist:
    - 'github/octocat'
schedule_allowlist:
    - '*'
created_at: 0
updated_at: 1715791151
updated_by: octocat
```

## Advanced

#### Input From File

Vela supports updating a settings record from a file using the `@` symbol.

```sh
# Syntax
vela update settings --file @/path/to/file

# Example
vela update settings --file @$HOME/tmp/settings.yml
```

##### Single YAML document

```yaml
---
platform:
    compiler:
        clone_image: target/vela-git:latest
        template_depth: 3
        starlark_exec_limit: 7500
    queue:
        routes:
            - vela
    repo_allowlist:
        - 'github/octocat'
    schedule_allowlist:
        - '*'
    created_at: 0
    updated_at: 1715791151
    updated_by: octocat
```
