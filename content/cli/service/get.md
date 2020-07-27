---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list services.
---

## Command

```
$ vela get service <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get service --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                           | Environment Variables               |
| ---------- | ------------------------------------- | ----------------------------------- |
| `org`      | name of organization for the services | `VELA_ORG`, `SERVICE_ORG`           |
| `repo`     | name of repository for the services   | `VELA_REPO`, `SERVICE_REPO`         |
| `build`    | number of build for the services      | `VELA_BUILD`, `SERVICE_BUILD`       |
| `output`   | format the output for the services    | `VELA_OUTPUT`, `SERVICE_OUTPUT`     |
| `page`     | prints a specific page of services    | `VELA_PAGE`, `SERVICE_PAGE`         |
| `per.page` | number of services to print per page  | `VELA_PER_PAGE`, `SERVICE_PER_PAGE` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`
- `output`

For more information, please review the [CLI config documentation](/docs/cli/config/).
{{% /alert %}}

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/cli/authentication/).
{{% /alert %}}

#### Request

```sh
$ vela get service --org github --repo octocat --build 1
```

#### Response

```sh
NAME            STATUS  RUNTIME DURATION
publish         failure         1s
build           success         17s
test            success         10s
clone           success         2s
```
