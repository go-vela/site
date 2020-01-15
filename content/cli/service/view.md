---
title: "View"
linkTitle: "View"
weight: 10
description: >
  Learn how to view a service.
---

## Information

```sh
NAME:
   vela view service - View details of the provided service

USAGE:
   vela view service [command options] [arguments...]

DESCRIPTION:
   Use this command to view a service.
```

## Flags

```sh
OPTIONS:
   --org value               Provide the organization for the repository [$BUILD_ORG]
   --repo value              Provide the repository contained with the organization [$BUILD_REPO]
   --build-number value      Provide the build number (default: 0) [$BUILD_NUMBER]
   --service-number value       Provide the build number (default: 0) [$service_NUMBER]
   --output value, -o value  Print the output in json format
```

## Examples

```sh
EXAMPLES:
 1. Get service details for a repository.
    $ vela view service --org github --repo octocat --build-number 1 --service-number 1
 2. Get service details for a repository with json output.
    $ vela view service --org github --repo octocat --build-number 1 --service-number 1 --output json
 3. Get service details for a repository when org and repo config or environment variables are set.
    $ vela view service --build-number 1 --service-number 1
```

## Sample

```sh
$ vela view service --org github --repo octocat --build-number 5 --service-number 1

id: 1
buildid: 5
repoid: 1
number: 5
name: clone
status: success
error: ""           # Populates when the platform runs into an error with the build
exitcode: 0
created: 1561748980
started: 1561748979
finished: 1561748981
```
