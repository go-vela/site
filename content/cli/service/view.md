---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a service.
---

## Command

```
$ vela view service <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view service --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name      | Description          | Environment      |
| --------- | -------------------- | ---------------- |
| `org`     | name of organization | `BUILD_ORG`      |
| `repo`    | name of repository   | `BUILD_REPO`     |
| `build`   | number of build      | `BUILD_NUMBER`   |
| `service` | number of service    | `SERVICE_NUMBER` |
| `output`  | format the output    | `N/A`            |

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
$ vela view service --org github --repo octocat --build 1 --service 1
```

#### Response

```sh
id: 1
build_id: 1
repo_id: 1
number: 1
name: clone
status: success
error: ""
exitcode: 0
created: 1561748980
started: 1561748979
finished: 1561748981
```
