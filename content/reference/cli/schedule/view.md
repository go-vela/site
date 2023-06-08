---
title: "View"
linkTitle: "View"
description: >
  Learn how to inspect a schedule.
---

## Command

```
$ vela view schedule <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela view schedule --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                           | Environment Variables            |
|------------|---------------------------------------|----------------------------------|
| `org`      | name of organization for the schedule | `VELA_ORG`, `SCHEDULE_ORG`       |
| `repo`     | name of repository for the schedule   | `VELA_REPO`, `SCHEDULE_REPO`     |
| `schedule` | name of the schedule                  | `VELA_SCHEDULE`, `SCHEDULE_NAME` |
| `output`   | format the output for the schedule    | `VELA_OUTPUT`, `SCHEDULE_OUTPUT` |

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
$ vela view schedule --schedule hourly
```

#### Targeted Request

```sh
$ vela view schedule --org github --repo octocat --schedule hourly
```

#### Response
```sh
{
  Active: true,
  CreatedAt: 1641314085,
  CreatedBy: octokitty,
  Entry: 0 * * * *,
  ID: 1,
  Name: hourly,
  RepoID: 1,
  ScheduledAt: 0,
  UpdatedAt: 1641314085,
  UpdatedBy: octokitty,
}
```

## Examples

```sh
EXAMPLES:
  1. View details of a schedule for a repository.
    $ vela view schedule --org MyOrg --repo MyRepo --schedule hourly
  2. View details of a schedule for a repository with json output.
    $ vela view schedule --org MyOrg --repo MyRepo --schedule hourly --output json
  3. View details of a schedule for a repository when config or environment variables are set.
    $ vela view schedule
```