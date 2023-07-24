---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list schedules.
---

## Command

```
$ vela get schedule <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela get schedule --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name       | Description                            | Environment Variables                |
|------------|----------------------------------------|--------------------------------------|
| `org`      | name of organization for the schedules | `VELA_ORG`, `SCHEDULE_ORG`           |
| `repo`     | name of repository for the schedules   | `VELA_REPO`, `SCHEDULE_REPO`         |
| `output`   | format the output for the schedules    | `VELA_OUTPUT`, `SCHEDULE_OUTPUT`     |
| `page`     | prints a specific page of schedules    | `VELA_PAGE`, `SCHEDULE_PAGE`         |
| `per.page` | number of schedules to print per page  | `VELA_PER_PAGE`, `SCHEDULE_PER_PAGE` |

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
$ vela get schedule
```

#### Targeted Request

```sh
$ vela get schedule --org github --repo octocat
```

#### Response
```sh
NAME   	ENTRY    	ACTIVE	SCHEDULED_AT
nightly	0 0 * * *	true  	a second ago
hourly 	0 * * * *	true  	a second ago
```

## Examples

```sh
EXAMPLES:
  1. Get a list of schedules for a repository.
    $ vela get schedule --org MyOrg --repo MyRepo
  2. Get a list of schedules for a repository with wide view output.
    $ vela get schedule --org MyOrg --repo MyRepo --output wide
  3. Get a list of schedules for a repository with yaml output.
    $ vela get schedule --org MyOrg --repo MyRepo --output yaml
  4. Get a list of schedules for a repository with json output.
    $ vela get schedule --org MyOrg --repo MyRepo --output json
  5. Get a list of schedules for a repository when config or environment variables are set.
    $ vela get schedule
```