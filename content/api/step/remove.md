---
title: "Remove"
linkTitle: "Remove"
weight: 35
description: >
  Learn how to remove a step.
---

## Endpoint

```
DELETE /api/v1/repos/:org/:repo/builds/:build/steps/:step
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
| build | Number of build. |
| step | Number of step. |

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description |
|---|---|
| 200 | Indicates the request has succeeded. |
| 401 | Indicates the user does not have proper permissions. |

## Example Response Body

```
step github/octokitty/1/1 removed
```
