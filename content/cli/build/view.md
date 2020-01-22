---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a build.
---

## Command

```
$ vela view build <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view build --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment    |
| -------- | -------------------- | -------------- |
| `org`    | name of organization | `BUILD_ORG`    |
| `repo`   | name of repository   | `BUILD_REPO`   |
| `build`  | number of build      | `BUILD_NUMBER` |
| `output` | format the output    | `N/A`          |

{{% alert color="info" %}}
This command also supports setting the `org` or `repo` parameters via a configuration file.

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
vela view build --org github --repo octocat --number 1
```

#### Response

```sh
id: 1
repo_id: 1
number: 1
parent: 1
event: push
status: created
error: ""               # Populates when the platform runs into an error with the build
enqueued: 1563474077
created: 1563474076
started: 1563474077
finished: 0
deploy: ""
clone: https://github.com/github/octocat.git
source: https://github.com/github/octocat/commit/48afb5bdc41ad69bf22588491333f7cf71135163
title: push received from https://github.com/github/octocat
message: First commit...
commit: 48afb5bdc41ad69bf22588491333f7cf71135163
sender: OctoKitty
author: OctoKitty
branch: master
ref: refs/heads/master
baseref: ""
host: "company.localhost"
runtime: "docker"
distribution: "linux"
```
