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
$ vela add schedule --org github --repo octocat --schedule hourly --entry '0 * * * *' --output json
```

#### Response
```sh
{
	"id": 1,
	"repo": {
		"id": 1,
		"owner": {
			"id": 1,
			"name": "octokitty",
			"active": true
		},
		"org": "github",
		"name": "octokitty",
		"full_name": "github/octokitty",
		"link": "https://github.com/github/octokitty",
		"clone": "https://github.com/github/octokitty.git",
		"branch": "main",
		"topics": [],
		"build_limit": 10,
		"timeout": 30,
		"counter": 0,
		"visibility": "public",
		"private": false,
		"trusted": false,
		"active": true,
		"allow_events": {
			"push": {
				"branch": true,
				"tag": false,
				"delete_branch": false,
				"delete_tag": false
			},
			"pull_request": {
				"opened": false,
				"edited": false,
				"synchronize": false,
				"reopened": false,
				"labeled": false,
				"unlabeled": false
			},
			"deployment": {
				"created": false
			},
			"comment": {
				"created": false,
				"edited": false
			},
			"schedule": {
				"run": false
			}
		},
		"pipeline_type": "yaml",
		"previous_name": "",
		"approve_build": "fork-always"
	},
	"active": true,
	"name": "hourly",
	"entry": "0 * * * *",
	"created_at": 1716495910,
	"created_by": "octokitty",
	"updated_at": 1716495910,
	"updated_by": "octokitty",
	"scheduled_at": 0,
	"branch": "main",
	"error": "",
	"next_run": 1716499800
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