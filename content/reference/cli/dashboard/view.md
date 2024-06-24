---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a dashboard.
---

## Command

```
$ vela view dashboard <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view dashboard --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                                             | Environment Variables               |
| -------- | ------------------------------------------------------- | ----------------------------------- |
| `id`     | uuid for the dashboard                                  | `VELA_DASHBOARD_ID`, `DASHBOARD_ID` |
| `full`   | output the repo and build information for the dashboard | `VELA_FULL`, `DASHBOARD_FULL`       |
| `output` | format the output for the dashboard                     | `VELA_OUTPUT`, `REPO_OUTPUT`        |

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
$ vela view dashboard --id d3040cd7-9bb6-45d1-a2a1-d794483a902c
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
  1. View a dashboard.
    $ vela view dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8
  2. View a dashboard with repo and build information.
    $ vela view dashboard --id c8da1302-07d6-11ea-882f-4893bca275b8 --full
```
