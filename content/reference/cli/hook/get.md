---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list hooks.
---

## Command

```
$ vela get hook <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get hook --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                        | Environment Variables            |
| ---------- | ---------------------------------- | -------------------------------- |
| `org`      | name of organization for the hooks | `VELA_ORG`, `HOOK_ORG`           |
| `repo`     | name of repository for the hooks   | `VELA_REPO`, `HOOK_REPO`         |
| `output`   | format the output for the hooks    | `VELA_OUTPUT`, `HOOK_OUTPUT`     |
| `page`     | prints a specific page of hooks    | `VELA_PAGE`, `HOOK_PAGE`         |
| `per.page` | number of hooks to print per page  | `VELA_PER_PAGE`, `HOOK_PER_PAGE` |

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

<div class="highlight"><pre><code><b>~/github/octocat $</b> vela get hook</code></pre></div>

#### Targeted Request

<div class="highlight"><pre><code><b>~ $</b> vela get hook --org github --repo octocat</code></pre></div>

#### Response

```sh
NUMBER  STATUS  EVENT   BRANCH
5       failure push    master
4       failure push    master
3       success push    master
2       success push    master
1       success push    master
```
