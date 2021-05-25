---
title: "Cancel"
linkTitle: "Cancel"
description: >
  Learn how to cancel a build.
---

## Endpoint

```
DELETE  /api/v1/repos/:org/:repo/builds/:build/cancel
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                              |
| ----------- | ---------------------------------------------------------|
| `200`       | indicates the request has succeeded                      |
| `401`       | indicates the user does not have proper permissions      |
| `404`       | indicates that the server was unable to cancel the build |
| `500`       | indicates there was an error trying to cancel the build  | 

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
  "http://127.0.0.1:8080/api/v1/repos/github/octocat/builds/1/cancel"
```

#### Response

```json
  "canceled build github/octocat/36"
```
