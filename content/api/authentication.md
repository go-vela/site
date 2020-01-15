---
title: "Authentication"
linkTitle: "Authentication"
weight: 5
description: >
  Learn how to authentication to the API.
---

The API uses access tokens to authorize requests. You can retrieve an access token in the web or CLI user interfaces.

Authorization to the API is performed using the HTTP Authorization header. Provide your token as the bearer token value.

#### Example Header

```
Authorization: Bearer SOMEBEARERTOKEN
```

#### Example Request

```sh
curl -X GET "http://localhost:8080/api/v1/users" \
  -H "Authorization: Bearer SOMEBEARERTOKEN"
```
