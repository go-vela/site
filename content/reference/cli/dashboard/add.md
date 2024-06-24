---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a dashboard.
---

## Command

```
$ vela add dashboard <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela add dashboard --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                                       | Environment Variables                                   |
| ---------- | ------------------------------------------------- | ------------------------------------------------------- |
| `name`     | name for the dashboard                            | `VELA_DASHBOARD_NAME`, `DASHBOARD_NAME`                 |
| `repos`    | list of repositories (org/repo) for the dashboard | `VELA_DASHBOARD_REPOS`, `DASHBOARD_REPOS`               |
| `branches` | filter builds in all repositories by branch       | `VELA_DASHBOARD_REPOS_BRANCH`, `DASHBOARD_REPOS_BRANCH` |
| `events`   | filter builds in all repositories by event        | `VELA_DASHBOARD_REPOS_EVENT`, `DASHBOARD_REPOS_EVENT`   |
| `admins`   | provide the list of admins for the dashboard      | `VELA_DASHBOARD_ADMINS`, `DASHBOARD_ADMINS`             |
| `output`   | format the output for the dashboard               | `VELA_OUTPUT`, `REPO_OUTPUT`                            |

{{% alert color="info" %}}
This command also supports setting the following parameters via a configuration file:

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
$ vela add dashboard --name 'Octocat Main Branches' --repos octocat/Hello-World,octocat/Spoon-Knife --branches main
```

#### Response

```sh
{
  Name: Octocat Main Branches,
  ID: d3040cd7-9bb6-45d1-a2a1-d794483a902c,
  Admins: [{
  Active: true,
  Admin: false,
  Dashboards: [],
  Favorites: [],
  ID: 1,
  Name: octokitty,
  Token: ,
}],
  CreatedAt: 1716572402,
  CreatedBy: octokitty,
  UpdatedAt: 1716572402,
  UpdatedBy: octokitty,
  Repos: [{
  Name: octocat/Hello-World,
  ID: 1,
  Branches: [main],
  Events: [],
} {
  Name: octocat/Spoon-Knife,
  ID: 2,
  Branches: [main],
  Events: [],
}],
}
```

## Examples

```sh
EXAMPLES:
  1. Add a dashboard.
    $ vela add dashboard --name my-dashboard
  2. Add a dashboard with repositories.
    $ vela add dashboard --name my-dashboard --repos Org-1/Repo-1,Org-2/Repo-2
  3. Add a dashboard with repositories filtering builds by pushes to main.
    $ vela add dashboard --name my-dashboard --repos Org-1/Repo-1,Org-2/Repo-2 --branch main --event push
  4. Add a dashboard with multiple admins.
    $ vela add dashboard --name my-dashboard --admins JohnDoe,JaneDoe
```
