---
title: "Remove"
linkTitle: "Remove"
weight: 35
description: >
  Learn how to remove a service.
---

## Endpoint

```
DELETE /api/v1/repos/:org/:repo/builds/:build/services/:service
```

| Param | Description |
|---|---|
| org | Name of organization. |
| repo | Name of repository. |
| build | Number of build. |
| service | Number of service. |

## Permissions

Documentation Coming Soon!

## Response codes

| Status Code | Description |
|---|---|
| 200 | Indicates the request has succeeded. |
| 401 | Indicates the user does not have proper permissions. |

## Example Response Body

```
service github/octokitty/1/1 removed
```
