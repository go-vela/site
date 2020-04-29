---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a deployment.
---

## Command

```
$ vela add deployment <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela add deployment --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name          | Description                   | Environment        |
| ------------- | ----------------------------- | ------------------ |
| `org`         | name of organization          | `VELA_ORG`         |
| `repo`        | name of repository            | `VELA_NAME`        |
| `ref`         | name of branch, commit or tag | `VELA_REF`         |
| `target`      | name of target environment    | `VELA_TARGET`      |
| `description` | description for deployment    | `VELA_DESCRIPTION` |
| `task`        | name of task                  | `VELA_TASK`        |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`

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
vela add deployment --org github --repo octocat
```

#### Response

```sh
deployment "https://api.github.com/repos/github/octocat/deployments/1" was created
```
