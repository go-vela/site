---
title: "Get"
linkTitle: "Get"
weight: 10
description: >
  Learn how to get repos.
---

## Information

```sh
NAME:
   vela get repo - Display a list of repositories

USAGE:
   vela get repo [command options] [arguments...]

DESCRIPTION:
   Use this command to get a list of repositories.
```

## Flags

```sh
OPTIONS:
   --output value, -o value  Print the output in wide, yaml or json format
```

## Examples

```sh
EXAMPLES:
 1. Get repositories.
    $ vela get repo
 2. Get repositories with wide view output.
    $ vela get repo --output wide
 3. Get repositories with yaml output.
    $ vela get repo --output yaml
 4. Get repositories with json output.
    $ vela get repo --output json
```

## Sample

```sh
$ vela get repo

ORG/REPO        STATUS  EVENTS             VISIBILITY  BRANCH
github/octocat  true    push,pull_request  public      master
```
