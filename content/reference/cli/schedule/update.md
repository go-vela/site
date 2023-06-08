---
title: "Update"
linkTitle: "Update"
description: >
  Learn how to modify a schedule.
---

## Command

```
$ vela update schedule <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela update schedule --help`.
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

## Permissions

COMING SOON!

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
$ vela update schedule --name hourly --active false
```

#### Targeted Request

```sh
$ vela update schedule --org github --repo octocat --name hourly --active false
```

#### Response

```sh
{
  Active: false,
  CreatedAt: 1641314085,
  CreatedBy: octokitty,
  Entry: 0 * * * *,
  ID: 1,
  Name: hourly,
  RepoID: 1,
  ScheduledAt: 0,
  UpdatedAt: 1641314086,
  UpdatedBy: octokitty,
}
```

## Examples

```sh
EXAMPLES:
  1. Update a schedule for a repository with active disabled.
    $ vela update schedule --org MyOrg --repo MyRepo --schedule hourly --active false
  2. Update a schedule for a repository with a new entry.
    $ vela update schedule --org MyOrg --repo MyRepo --schedule nightly --entry '@nightly'
  3. Update a schedule for a repository when config or environment variables are set.
    $ vela update schedule
```