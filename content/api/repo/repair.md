---
title: "Repair"
linkTitle: "Repair"
weight: 20
description: >
  Learn how to repair a repo.
---

## Endpoint

```
PATCH /api/v1/repos/:org/:repo/repair
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
repo github/octokitty repaired
```
