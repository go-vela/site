---
title: "Update"
linkTitle: "Update"
weight: 20
description: >
  Learn how to update a repo.
---

## Information

```sh
NAME:
   vela update repo - Update a repository

USAGE:
   vela update repo [command options] [arguments...]

DESCRIPTION:
   Use this command to update a repository.
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
 1. Update a repository.
    $ vela update repo --org github --repo octocat
 2. Update a repository with all event types enabled.
    $ vela update repo --org github --repo octocat --event push --event pull_request --event tag --event deployment
 3. Update a repository with a longer build timeout.
    $ vela update repo --org github --repo octocat --timeout 90
 4. Update a repository when org and repo config or environment variables are set.
    $ vela update repo
```

## Sample

```sh
$ vela update repo --org github --repo octocat --event push --event pull_request --event deployment

repo "github/octocat" was updated
```
