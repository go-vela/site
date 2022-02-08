---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list deployments.
---

## Command

```
$ vela get deployment <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get deployment --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                              | Environment Variables                  |
| ---------- | ---------------------------------------- | -------------------------------------- |
| `org`      | name of organization for the deployments | `VELA_ORG`, `DEPLOYMENT_ORG`           |
| `repo`     | name of repository for the deployments   | `VELA_REPO`, `DEPLOYMENT_REPO`         |
| `output`   | format the output for the deployments    | `VELA_OUTPUT`, `DEPLOYMENT_OUTPUT`     |
| `page`     | prints a specific page of deployments    | `VELA_PAGE`, `DEPLOYMENT_PAGE`         |
| `per.page` | number of deployments to print per page  | `VELA_PER_PAGE`, `DEPLOYMENT_PER_PAGE` |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

- `org`
- `repo`
- `output`

For more information, please review the [CLI config documentation](/docs/reference/cli/config/).
{{% /alert %}}

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
$ vela get deployment
```

#### Targeted Request

```sh
$ vela get deployment --org github --repo octocat
```

#### Response generated from successful CLI command
```sh
ID  TASK         USER     REF     TARGET
2   deploy:vela  octocat  master  production
1   deploy:vela  octocat  master  production
```

## Examples

```sh
EXAMPLES:
  1. Get deployments for a repository.
    $ vela get deployment --org MyOrg --repo MyRepo
  2. Get deployments for a repository with wide view output.
    $ vela get deployment --org MyOrg --repo MyRepo --output wide
  3. Get deployments for a repository with yaml output.
    $ vela get deployment --org MyOrg --repo MyRepo --output yaml
  4. Get deployments for a repository with json output.
    $ vela get deployment --org MyOrg --repo MyRepo --output json
  5. Get deployments for a repository when config or environment variables are set.
    $ vela get deployment
```
