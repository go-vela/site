---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a secret.
---

## Command

```
$ vela view secret <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view secret --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name            | Description                           | Environment Variables          |
| --------------- | ------------------------------------- | ------------------------------ |
| `org`           | name of organization for the secret   | `VELA_ORG`, `SECRET_ORG`       |
| `repo`          | name of repository for the secret     | `VELA_REPO`, `SECRET_REPO`     |
| `secret.engine` | name of engine that stores the secret | `VELA_ENGINE`. `SECRET_ENGINE` |
| `secret.type`   | name of type of secret being stored   | `VELA_TYPE`, `SECRET_TYPE`     |
| `team`          | name of team for the secret           | `VELA_TEAM`, `SECRET_TEAM`     |
| `name`          | name of the secret                    | `VELA_NAME`, `SECRET_NAME`     |
| `output`        | format the output for the secret      | `VELA_OUTPUT`, `SECRET_OUTPUT` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `secret.engine`
- `secret.type`
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

<div class="highlight"><pre><code><b>~/github/octocat $</b> vela view secret --secret.engine native --secret.type repo --name foo</code></pre></div>

#### Targeted Request

<div class="highlight"><pre><code><b>~ $</b> vela view secret --secret.engine native --secret.type repo --org github --repo octocat --name foo</code></pre></div>

#### Response

```sh
id: 1
org: github
repo: octocat
team: ""
name: foo
value: "[secure]"
type: repo
images: null
events:
  - push
  - pull_request
```
