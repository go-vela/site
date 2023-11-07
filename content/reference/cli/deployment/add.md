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

| Name          | Description                                         | Environment Variables                        |
| ------------- | --------------------------------------------------- | -------------------------------------------- |
| `org`         | name of organization for the deployment             | `VELA_ORG`, `DEPLOYMENT_ORG`                 |
| `repo`        | name of repository for the deployment               | `VELA_REPO`, `DEPLOYMENT_REPO`               |
| `ref`         | name of branch, commit, or tag for the deployment   | `VELA_DEPLOYMENT`, `DEPLOYMENT_NUMBER`       |
| `target`      | name of target environment for the deployment       | `VELA_TARGET`, `DEPLOYMENT_TARGET`           |
| `description` | short description for the deployment                | `VELA_DESCRIPTION`, `DEPLOYMENT_DESCRIPTION` |
| `parameter`   | parameter(s) in key=value format for the deployment | `VELA_PARAMETERS,`, `DEPLOYMENT_PARAMETERS`  |
| `task`        | name of task for the deployment                     | `VELA_TASK`, `DEPLOYMENT_TASK`               |
| `output`      | format the output for the deployment                | `VELA_OUTPUT`, `DEPLOYMENT_OUTPUT`           |

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
$ vela add deployment
```

#### Targeted Request

```sh
$ vela add deployment --org github --repo octocat
```

#### Response generated from successful CLI command
```sh
deployment "https://api.github.com/repos/github/octocat/deployments/1" was created
```

## Examples

```sh
EXAMPLES:
  1. Add a deployment for a repository.
    $ vela add deployment --org MyOrg --repo MyRepo
  2. Add a deployment for a repository with a specific target environment.
    $ vela add deployment --org MyOrg --repo MyRepo --target stage
  3. Add a deployment for a repository with a specific branch reference.
    $ vela add deployment --org MyOrg --repo MyRepo --ref dev
  4. Add a deployment for a repository with a specific commit reference.
    $ vela add deployment --org MyOrg --repo MyRepo --ref 48afb5bdc41ad69bf22588491333f7cf71135163
  5. Add a deployment for a repository with a specific tag.
    $ vela add deployment --org MyOrg --repo MyRepo --ref 'refs/tags/example.tag'
  5. Add a deployment for a repository with a specific description.
    $ vela add deployment --org MyOrg --repo MyRepo --description 'my custom message'
  6. Add a deployment for a repository with two parameters.
    $ vela add deployment --org MyOrg --repo MyRepo --parameter 'key=value' --parameter 'foo=bar'
  7. Add a deployment for a repository when config or environment variables are set.
    $ vela add deployment
```
