---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a deployment.
---

## Command

```
$ vela view deployment <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view deployment --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name         | Description                             | Environment Variables                  |
| ------------ | --------------------------------------- | -------------------------------------- |
| `org`        | name of organization for the deployment | `VELA_ORG`, `DEPLOYMENT_ORG`           |
| `repo`       | name of repository for the deployment   | `VELA_REPO`, `DEPLOYMENT_REPO`         |
| `deployment` | number of the deployment                | `VELA_DEPLOYMENT`, `DEPLOYMENT_NUMBER` |
| `output`     | format the output for the deployment    | `VELA_OUTPUT`, `DEPLOYMENT_OUTPUT`     |

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
vela view deployment --org github --repo octocat --deployment 1
```

#### Response

```sh
id: 1
repo_id: 1
url: https://api.github.com/repos/github/octocat/deployments/1
user: octocat
commit: 48afb5bdc41ad69bf22588491333f7cf71135163
ref: master
task: deploy:vela
target: production
description: Deployment request from Vela
```
