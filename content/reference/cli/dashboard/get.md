---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list dashboards.
---

## Command

```
$ vela get dashboard <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get dashboard --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                                             | Environment Variables             |
| -------- | ------------------------------------------------------- | --------------------------------- |
| `full`   | output the repo and build information for the dashboard | `VELA_FULL`, `DASHBOARD_FULL`     |
| `output` | format the output for dashboards                        | `VELA_OUTPUT`, `DASHBOARD_OUTPUT` |

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
$ vela get dashboard
```

#### Response

```sh
[{
  Name: Octocat Main Branches,
  ID: 59376e53-879f-478e-b6d2-b8aefe219c6d,
  Admins: [{
  Active: true,
  Admin: false,
  Dashboards: [],
  Favorites: [],
  ID: 1,
  Name: octokitty,
  Token: ,
}],
  CreatedAt: 1715117480,
  CreatedBy: octokitty,
  UpdatedAt: 1715117480,
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
} {
  Name: Octocat PR Events,
  ID: 0ebb9f01-389c-4a0f-b301-6bf2f9a0fe3b,
  Admins: [{
  Active: true,
  Admin: false,
  Dashboards: [],
  Favorites: [],
  ID: 1,
  Name: octokitty,
  Token: ,
}],
  CreatedAt: 1716397739,
  CreatedBy: octokitty,
  UpdatedAt: 1716397739,
  UpdatedBy: octokitty,
  Repos: [{
  Name: octocat/Hello-World,
  ID: 1,
  Branches: [],
  Events: [pull_request],
} {
  Name: octocat/Spoon-Knife,
  ID: 2,
  Branches: [],
  Events: [pull_request],
}],
}]
```

## Examples

```sh
EXAMPLES:
  1. Get user dashboards.
    $ vela get dashboard
  2. Get user dashboards with repo and build information.
    $ vela get dashboard --full
```
