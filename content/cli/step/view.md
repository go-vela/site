---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a step.
---

## Command

```
$ vela view step <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view step --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description          | Environment    |
| -------- | -------------------- | -------------- |
| `org`    | name of organization | `BUILD_ORG`    |
| `repo`   | name of repository   | `BUILD_REPO`   |
| `build`  | number of build      | `BUILD_NUMBER` |
| `step`   | number of step       | `STEP_NUMBER`  |
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
vela view step --org github --repo octocat --build 1 --step 1
```

#### Response

```sh
id: 1
build_id: 1
repo_id: 1
number: 1
name: clone
status: success
error: ""           # Populates when the platform runs into an error with the build
exitcode: 0
created: 1561748980
started: 1561748979
finished: 1561748981
host: "worker.host.com"
runtime: "docker"
distribution: "linux"
```
