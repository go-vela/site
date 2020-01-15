---
title: "Remove"
linkTitle: "Remove"
weight: 20
description: >
  Learn how to remove a repo.
---

## Information

```sh
NAME:
   vela remove repo - Remove a repository

USAGE:
   vela remove repo [command options] [arguments...]

DESCRIPTION:
   Use this command to remove a repository.
```

## Flags

```sh
OPTIONS:
   --org value   Provide the organization for the repository [$REPO_ORG]
   --repo value  Provide the repository contained with the organization [$REPO_NAME]
```

## Examples

```sh
EXAMPLES:
 1. Remove a repository.
    $ vela remove repo --org github --repo octocat
 2. Remove a repository when org and repo config or environment variables are set.
    $ vela remove repo
```

## Sample

```sh
$ vela delete repo --org github --repo octocat

repo "github/octocat" was deleted
```
