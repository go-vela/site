---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect platform settings.
---

## Command

```
$ vela view settings
```

{{% alert color="info" %}}
For more information, you can run `vela view settings --help`.
{{% /alert %}}

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
$ vela view settings
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
