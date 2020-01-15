---
title: "View"
linkTitle: "View"
weight: 5
description: >
  Learn how to view logs.
---

## Information

```sh
NAME:
   vela view log - View logs from the provided build or step

USAGE:
   vela view log [command options] [arguments...]

DESCRIPTION:
   Use this command to capture the logs from a build or step.
```

## Flags

```sh
OPTIONS:
   --org value                           Provide the organization for the repository [$BUILD_ORG]
   --repo value                          Provide the repository contained with the organization [$BUILD_REPO]
   --build-number value, --number value  Print the output in wide, yaml or json format (default: 0) [$BUILD_NUMBER]
   --step-name value, --sn value         name for which you want to filter the logs [$LOG_STEP_NAME]
```

## Examples

```sh
EXAMPLES:
 1. View build logs for a repository.
    $ vela view log --org github --repo octocat --number 1
 2. View step logs for a build for a repository.
    $ vela view log --step validate --org github --repo octocat --number 1
 3. View build logs for a repository when org and repo config or environment variables are set.
    $ vela view log --number 1
```

## Sample

```sh
$ vela view log --org github --repo octocat --number 5

$ git init
Initialized empty Git repository in /home/github_octocat_5/.git/
$ git remote add origin https://github.com/github/octocat.git
$ git remote --verbose
origin  https://github.com/github/octocat.git (fetch)
origin  https://github.com/github/octocat.git (push)
$ git fetch --no-tags origin refs/heads/master
From https://github.com/github/octocat
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
$ git reset --hard afafce5e33a8efd4340613b31a953107d6dec3a3
HEAD is now at afafce5 Dummy commit

$ echo "Hello World!"
Hello World!
```
