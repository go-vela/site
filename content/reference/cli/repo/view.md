---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a repo.
---

## Command

```
$ vela view repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                             | Environment Variables        |
| -------- | --------------------------------------- | ---------------------------- |
| `org`    | name of organization for the repository | `VELA_ORG`, `REPO_ORG`       |
| `repo`   | name of repository                      | `VELA_REPO`, `REPO_NAME`     |
| `output` | format the output for the repository    | `VELA_OUTPUT`, `REPO_OUTPUT` |

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
$ vela view repo
```

#### Targeted Request

```sh
$ vela view repo --org github --repo octocat
```

#### Response

```sh
id: 1
userid: 1
org: github
name: octocat
fullname: github/octocat
link: https://github.com/github/octocat
clone: https://github.com/github/octocat.git
branch: master
timeout: 60
counter: 0
visibility: public
private: false
trusted: false
active: true
allowpull: true
allowpush: true
allowdeploy: false
allowtag: false
allowcomment: false
```
