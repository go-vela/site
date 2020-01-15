---
title: "View"
linkTitle: "View"
weight: 10
description: >
  Learn how to view a build.
---

## Information

```sh
NAME:
   vela view build - View details of the provided build

USAGE:
   vela view build [command options] [arguments...]

DESCRIPTION:
   Use this command to view a build.
```

## Flags

```sh
OPTIONS:
   --org value                                    Provide the organization for the repository [$BUILD_ORG]
   --repo value                                   Provide the repository contained within the organization [$BUILD_REPO]
   --build-number value, --build value, -b value  Provide the build number (default: 0) [$BUILD_NUMBER]
   --output value, -o value                       Print the output in json format
```

## Examples

```sh
EXAMPLES:
 1. View build details for a repository.
    $ vela view build --org github --repo octocat --build-number 1
 2. View build details for a repository with json output.
    $ vela view build --org github --repo octocat --build-number 1 --output json
 3. View build details for a repository when org and repo config or environment variables are set.
    $ vela view build --build-number 1
```

## Sample

```sh
$ vela view build --org github --repo octocat --number 5

id: 3349
repositoryid: 1
number: 5
parent: 4
event: push
status: failure
error: ""               # Populates when the platform runs into an error with the build
enqueued: 1561748976
created: 1561748976
started: 1561748975
finished: 1561749020
deploy: ""
clone: https://github.com/github/octocat.git
source: https://github.com/github/octocat/commit/afafce5e33a8efd4340613b31a953107d6dec3a3
title: push received from https://github.com/github/octocat
message: Dummy commit
commit: afafce5e33a8efd4340613b31a953107d6dec3a3
sender: SimonOxley
author: SimonOxley
branch: master
ref: refs/heads/master
baseref: ""
host: "worker.host.com"
runtime: "docker"
distribution: "linux"
```
