---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list pipelines.
---

## Command

```
$ vela get pipeline <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get pipeline --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                            | Environment Variables            |
| ---------- |----------------------------------------| -------------------------------- |
| `org`      | name of organization for the pipelines | `VELA_ORG`, `HOOK_ORG`           |
| `repo`     | name of repository for the pipelines   | `VELA_REPO`, `HOOK_REPO`         |
| `output`   | format the output for the pipelines    | `VELA_OUTPUT`, `HOOK_OUTPUT`     |
| `page`     | prints a specific page of pipelines    | `VELA_PAGE`, `HOOK_PAGE`         |
| `per.page` | number of pipelines to print per page  | `VELA_PER_PAGE`, `HOOK_PER_PAGE` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`
- `output`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
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
$ vela get pipeline
```

#### Targeted Request

```sh
$ vela get pipeline --org github --repo octocat
```

#### Response

```sh
COMMIT                                     REF                 TYPE   VERSION   STAGES   STEPS
a49aaf4afae6431a79239c95247a2b169fd9f067   refs/heads/main   yaml   1         f        t
48afb5bdc41ad69bf22588491333f7cf71135163   refs/heads/main   yaml   1         f        t
```
