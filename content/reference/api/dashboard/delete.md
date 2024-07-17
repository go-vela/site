---
title: "Delete"
linkTitle: "Delete"
description: >
  Learn how to delete a dashboard.
---

## Endpoint

```
DELETE  /api/v1/dashboards/:id
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `400`       | indicates a bad request                             |
| `401`       | indicates the user does not have proper permissions |
| `500`       | indicates a server error                            |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X DELETE \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d "@data.json" \
  "http://127.0.0.1:8080/api/v1/dashboards/f460e0a1-a6a5-4724-89e8-4b2b39e12012"
```

#### Response

```
"dashboard test deleted"
```