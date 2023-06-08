---
title: "Add"
linkTitle: "Add"
description: >
  Learn how to create a schedule.
---

## Command

```
$ vela add schedule <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela add schedule --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                           | Environment Variables            |
|------------|---------------------------------------|----------------------------------|
| `org`      | name of organization for the schedule | `VELA_ORG`, `SCHEDULE_ORG`       |
| `repo`     | name of repository for the schedule   | `VELA_REPO`, `SCHEDULE_REPO`     |
| `schedule` | name of the schedule                  | `VELA_SCHEDULE`, `SCHEDULE_NAME` |
| `entry`    | frequency for the schedule            | `VELA_ENTRY`, `SCHEDULE_ENTRY`   |
| `active`   | enables/disables the schedule         | `VELA_ACTIVE`, `SCHEDULE_ACTIVE` |
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
$ vela add schedule --schedule hourly --entry '0 * * * *'
```

#### Targeted Request

```sh
$ vela add schedule --org github --repo octocat --schedule hourly --entry '0 * * * *'
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
  1. Add a schedule to a repository with active not enabled.
    $ vela add schedule --org MyOrg --repo MyRepo --schedule hourly --entry '0 * * * *' --active false
  2. Add a schedule to a repository with a nightly entry.
    $ vela add schedule --org MyOrg --repo MyRepo --schedule nightly --entry '0 0 * * *'
  3. Add a schedule to a repository with a weekly entry.
    $ vela add schedule --org MyOrg --repo MyRepo --schedule weekly --entry '@weekly'
  4. Add a schedule to a repository when config or environment variables are set.
    $ vela add schedule
```