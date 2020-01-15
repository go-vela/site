---
title: "Add"
linkTitle: "Add"
weight: 5
description: >
  Learn how to add a repo.
---

## Information

```sh
NAME:
   vela add repo - Add a repository

USAGE:
   vela add repo [command options] [arguments...]

DESCRIPTION:
   Use this command to add a repository.
```

## Flags

```sh
OPTIONS:
   --org value      Provide the organization for the repository [$REPO_ORG]
   --repo value     Provide the repository contained with the organization [$REPO_NAME]
   --link value     Link to repository in source control [$REPO_LINK]
   --clone value    Clone link to repository in source control [$REPO_CLONE]
   --timeout value  Allow management of timeouts (default: 60) [$REPO_TIMEOUT]
   --private        Allow management of private repositories [$REPO_PRIVATE]
   --trusted        Allow management of trusted repositories [$REPO_TRUSTED]
   --active         Allow management of activity on repositories [$REPO_ACTIVE]
   --event value    Allow management of the repository trigger events [$REPO_EVENT]
```

## Examples

```sh
EXAMPLES:
 1. Add a repository with push and pull request enabled.
    $ vela add repo --org github --repo octocat --event push --event pull_request
 2. Add a repository with all event types enabled.
    $ vela add repo --org github --repo octocat --event push --event pull_request --event tag --event deployment
 3. Add a repository with a longer build timeout.
    $ vela add repo --org github --repo octocat --timeout 90
 4. Add a repository with push and pull request enabled when org and repo config or environment variables are set.
    $ vela add repo --event push --event pull_request
```

## Sample

```sh
$ vela add repo --org github --repo octocat

repo "github/octocat" was created
```
