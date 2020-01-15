---
title: "Remove"
linkTitle: "Remove"
weight: 35
description: >
  Learn how to remove a repo.
---

## Endpoint

```
DELETE /api/v1/repos/:org/:repo
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description |
|---|---|
| 200 | Indicates the request has succeeded. |
| 401 | Indicates the user does not have proper permissions. |

## Example Response Body

```
removed github/octokitty
```
