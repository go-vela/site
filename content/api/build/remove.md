---
title: "Remove"
linkTitle: "Remove"
weight: 35
description: >
  Learn how to remove a build.
---

## Endpoint

```
DELETE /api/v1/repos/:org/:repo/builds/:build
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
| build | Number of build. |

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description |
|---|---|
| 200 | Indicates the request has succeeded. |
| 401 | Indicates the user does not have proper permissions. |

## Example Response Body

```
build github/octokitty/1 removed
```
