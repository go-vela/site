---
title: "Scheduling a Build"
linkTitle: "Scheduling a Build"
description: >
  Schedule builds for your repo.
---

{{% alert title="Note:" color="primary" %}}
Please ensure you've already [started a build](/docs/usage/start_build/) for your repo before attempting to setup a schedule.
{{% /alert %}}

Vela supports the ability to periodically trigger builds for a repo known as a "schedule".

Outside of the Vela ecosystem, this is more commonly known as a [cron expression](https://en.wikipedia.org/wiki/Cron).

Users will be able to manage schedules for a repo via the UI, [API](/docs/reference/api/schedule/) and [CLI](/docs/reference/api/schedule/).

Only users with `admin` access to a repo will be able to manage schedules for that repo.

{{% alert title="Warning:" color="primary" %}}
We make best efforts to support feature parity with `cron` but we may not support every capability.
{{% /alert %}}

## Entry

Users will be able to customize the cadence or frequency for how often the schedule should trigger a build via the `entry` field.

Here's a small list of examples to demonstrate valid values for this field:

* `0 * * * *` - setup a schedule to run every hour
* `0 0 * * *` - setup a schedule to run every day at midnight
* `0 0 * * 0` - setup a schedule to run every week on Sunday at midnight

Vela currently uses [github.com/adhocore/gronx](https://github.com/adhocore/gronx) to parse and validate this field.

This library also supports a number of "common cron expressions" (a.k.a. "tags") i.e. `@hourly`, `@daily`, `@weekly` etc.

For more information, please see that library's [official docs for these tags](https://github.com/adhocore/gronx#tags).

{{% alert title="Tip:" color="primary" %}}
We recommend leveraging an official cron expression generator like [Crontab Guru](https://crontab.guru/) to build the `entry` for your schedule.
{{% /alert %}}

## Pipeline

Uses will be able to customize what [stages](/docs/tour/stages/) or [steps](/docs/tour/steps/) will run in a build for a schedule using a [ruleset](/docs/tour/rulesets/):

```yaml
version: "1"

steps:
  - name: unit-test
    ruleset:
      event: [ deployment, schedule ]
      target: [ unit_test, integration_test, nightly ]
    commands:
      - echo "I run when a schedule with the name 'unit_test', 'integration_test' or 'nightly' is executed"

  - name: integration-test
    ruleset:
      event: [ deployment, schedule ]
      target: [ integration_test, nightly ]
    commands:
      - echo "I run when a schedule with the name 'integration_test' or 'nightly' is executed"
      
  - name: publish
    ruleset:
      event: [ deployment, schedule ]
      target: [ nightly ]
    commands:
      - echo "I run when a schedule with the name 'nightly' is executed"
      
  - name: notification
    ruleset:
      event: [ deployment, schedule ]
    commands:
      - echo "I run when any schedule is executed"
```

{{% alert title="Tip:" color="primary" %}}
We recommend adding the `deployment` event to your `ruleset` for processes that you want to run on a schedule.

This will enable you to manually trigger a build that replicates the configuration you want to run on a schedule.

This is especially useful when attempting to initially test and debug your pipeline for a schedule.
{{% /alert %}}