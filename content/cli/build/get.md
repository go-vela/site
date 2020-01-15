---
title: "Get"
linkTitle: "Get"
weight: 5
description: >
  Learn how to get builds.
---

## Information

```sh
NAME:
   vela get build - Display a list of builds

USAGE:
   vela get build [command options] [arguments...]

DESCRIPTION:
   Use this command to get a list of builds.
```

## Flags

```sh
OPTIONS:
   --org value               Provide the organization for the repository [$BUILD_ORG]
   --repo value              Provide the repository contained within the organization [$BUILD_REPO]
   --output value, -o value  Print the output in wide, yaml or json format
```

## Examples

```sh
EXAMPLES:
 1. Get builds for a repository.
    $ vela get build --org github --repo octocat
 2. Get builds for a repository with wide view output.
    $ vela get build --org github --repo octocat --output wide
 3. Get builds for a repository with yaml output.
    $ vela get build --org github --repo octocat --output yaml
 4. Get builds for a repository with json output.
    $ vela get build --org github --repo octocat --output json
 5. Get builds for a repository when org and repo config or environment variables are set.
    $ vela get build
```

## Sample

```sh
$ vela get build --org github --repo octocat

NUMBER  STATUS  EVENT   BRANCH  DURATION
5       failure push    master  45s
4       failure push    master  50s
3       success push    master  54s
2       success push    master  55s
1       pending push    master  ...
```
