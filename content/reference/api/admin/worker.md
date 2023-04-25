---
title: "Worker"
linkTitle: "Worker"
description: >
  Learn how to request a worker registration token as an admin.
---

## Endpoint

```
POST  /api/v1/admin/workers/:worker/register-token
```

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X PUT \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  "http://127.0.0.1:8080/api/v1/admin/workers/worker_1/register-token"
```

#### Response

```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ3b3JrZXJfMSIsImlhdCI6MTUxNjIzOTAyMiwiZWF0IjoxNTE2MjQ1MDIyLCJ0b2tlbl90eXBlIjoiV29ya2VyUmVnaXN0ZXIifQ.U2zNa3E8Wwd6ndoVMrwEZ1TWlmMVTZP8-UaShZA1Qpw" 
}
```