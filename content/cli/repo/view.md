---
title: "View"
linkTitle: "View"
weight: 15
description: >
  Learn how to view a repo.
---

## Information

```sh
NAME:
   vela view repo - View details of the provided repository

USAGE:
   vela view repo [command options] [arguments...]

DESCRIPTION:
   Use this command to view a repository.
```

## Flags

```sh
OPTIONS:
   --org value               Provide the organization for the repository [$REPO_ORG]
   --repo value              Provide the repository contained with the organization [$REPO_NAME]
   --output value, -o value  Print the output in json format
```

## Examples

```sh
EXAMPLES:
 1. View repository details.
    $ vela view repo --org github --repo octocat
 2. View repository details with json output.
    $ vela view repo --org github --repo octocat --output json
 3. View repository details when org and repo config or environment variables are set.
    $ vela view repo
```

## Sample

```sh
$ vela view repo --org github --repo octocat

id: 1
userid: 1
org: github
name: octocat
fullname: github/octocat
link: https://github.com/github/octocat
clone: https://github.com/github/octocat.git
branch: master
timeout: 60
visibility: public
private: false
trusted: false
active: true
allowpull: true
allowpush: true
allowdeploy: false
allowtag: false
```
