---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a repo.
---

## Command

```
$ vela update repo <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update repo --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name         | Description                                        | Environment Variables                |
| ------------ | -------------------------------------------------- | ------------------------------------ |
| `org`        | name of organization for the repository            | `VELA_ORG`, `REPO_ORG`               |
| `repo`       | name of repository                                 | `VELA_REPO`, `REPO_NAME`             |
| `link`       | full URL for the repository                        | `VELA_LINK`, `REPO_LINK`             |
| `branch`     | default branch for the repository                  | `VELA_BRANCH`, `REPO_BRANCH`         |
| `clone`      | clone URL for the repository                       | `VELA_CLONE`, `REPO_CLONE`           |
| `visibility` | access level required to view the repository       | `VELA_VISIBILITY`, `REPO_VISIBILITY` |
| `timeout`    | max time allowed per build                         | `VELA_TIMEOUT`, `REPO_TIMEOUT`       |
| `counter`    | set a value for a new build number                 | `VELA_COUNTER`, `REPO_COUNTER`       |
| `private`    | disables public access to the repository           | `VELA_PRIVATE`, `REPO_PRIVATE`       |
| `trusted`    | elevates permissions for builds for the repository | `VELA_TRUSTED`, `REPO_TRUSTED`       |
| `active`     | enables/disables the repository                    | `VELA_ACTIVE`, `REPO_ACTIVE`         |
| `event`      | events to trigger builds for the repository        | `VELA_EVENTS`, `REPO_EVENTS`         |
| `output`     | format the output for the repository               | `VELA_OUTPUT`, `REPO_OUTPUT`         |

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
vela update repo --org github --repo octocat --event tag
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
allowtag: true
allowcomment: false
```
