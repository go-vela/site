---
title: "Remove"
linkTitle: "Remove"
description: >
  Learn how to delete a schedule.
---

## Command

```
$ vela remove schedule <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela remove schedule --help`.
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
$ vela remove schedule --schedule hourly 
```

#### Targeted Request

```sh
$ pwd
~/github/octocat
$ vela remove schedule --org github --repo octocat --schedule hourly 
```

#### Response

```sh
schedule hourly deleted
```

## Examples

```sh
EXAMPLES:
  1. Remove a schedule from a repository.
    $ vela remove schedule --org MyOrg --repo MyRepo --schedule daily
  2. Remove a schedule from a repository with json output.
    $ vela remove schedule --org MyOrg --repo MyRepo --schedule daily --output json
  3. Remove a schedule from a repository when config or environment variables are set.
    $ vela remove schedule
```