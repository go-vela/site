---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a dashboard.
---

## Command

```
$ vela update dashboard <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update dashboard --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name           | Description                                                  | Environment Variables                                   |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
| `id`           | uuid for the dashboard                                       | `VELA_DASHBOARD_ID`, `DASHBOARD_ID`                     |
| `name`         | name for the dashboard                                       | `VELA_DASHBOARD_NAME`, `DASHBOARD_NAME`                 |
| `add-repos`    | list of repositories to add for the dashboard                | `VELA_DASHBOARD_ADD_REPOS`, `DASHBOARD_ADD_REPOS`       |
| `drop-repos`   | list of repositories to remove from the dashboard            | `VELA_DASHBOARD_DROP_REPOS`, `DASHBOARD_DROP_REPOS`     |
| `target-repos` | list of repositories to target for updates for the dashboard | `VELA_DASHBOARD_TARGET_REPOS`, `DASHBOARD_TARGET_REPOS` |
| `add-admins`   | list of admins to add for the dashboard                      | `VELA_DASHBOARD_ADD_ADMINS`, `DASHBOARD_ADD_ADMINS`     |
| `drop-admins`  | list of admins to remove from the dashboard                  | `VELA_DASHBOARD_DROP_ADMINS`, `DASHBOARD_DROP_ADMINS`   |
| `branches`     | filter builds in all repositories by branch                  | `VELA_DASHBOARD_REPOS_BRANCH`, `DASHBOARD_REPOS_BRANCH` |
| `events`       | filter builds in all repositories by event                   | `VELA_DASHBOARD_REPOS_EVENT`, `DASHBOARD_REPOS_EVENT`   |
| `output`       | format the output for the dashboard                          | `VELA_OUTPUT`, `DASHBOARD_OUTPUT`                       |

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
$ vela update dashboard --id d3040cd7-9bb6-45d1-a2a1-d794483a902c --name 'Octocat Dev Branches' --target-repos octocat/Hello-world,octocat/Spoon-Knife --branches dev
```

#### Response

```sh
{
  Name: Octocat Dev Branches,
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
  Branches: [dev],
  Events: [],
} {
  Name: octocat/Spoon-Knife,
  ID: 2,
  Branches: [dev],
  Events: [],
}],
}
```

## Examples

```sh
EXAMPLES:
  1. Update a dashboard to add a repository.
    $ vela update dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --add-repos Org-1/Repo-1
  2. Update a dashboard to remove a repository.
    $ vela update dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --drop-repos Org-1/Repo-1
  3. Update a dashboard to add event and branch filters to specific repositories.
    $ vela update dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --target-repos Org-1/Repo-1,Org-2/Repo-2 --branches main --events push
  4. Update a dashboard to change the name.
    $ vela update dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --name MyDashboard
  5. Update a dashboard to add an admin.
    $ vela update dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --add-admins JohnDoe
  6. Update a dashboard to remove an admin.
    $ vela update dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --drop-admins JohnDoe
```
