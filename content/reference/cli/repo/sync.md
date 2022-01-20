---
title: "Sync"
linkTitle: "Sync"
description: >
  Learn how to sync repos in database with GitHub.
---

## Command

```
$ vela sync repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela sync repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                             | Environment Variables        |
| -------- | --------------------------------------- | ---------------------------- |
| `org`    | name of organization for the repository | `VELA_ORG`, `REPO_ORG`       |
| `repo`   | name of repository                      | `VELA_REPO`, `REPO_NAME`     |
| `all`    | bool flag to sync all repos in an org   | `VELA_SYNC_ALL`, `SYNC_ALL`  |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

## Samples

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

<div class="highlight"><pre><code><b>~/github/octocat $</b> vela sync repo</code></pre></div>

#### Targeted Request

<div class="highlight"><pre><code><b>~ $</b> vela sync repo --org github --repo octocat</code></pre></div>

#### Response

```sh
repo "github/octocat" synced
```

#### Request

<div class="highlight"><pre><code><b>~/github/octocat $</b> vela sync repo --all</code></pre></div>

#### Targeted Request

<div class="highlight"><pre><code><b>~ $</b> vela sync repo --org github --all</code></pre></div>

#### Response

```sh
org "github" synced