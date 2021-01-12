---
title: "Authentication"
linkTitle: "Authentication"
weight: 5
description: >
  Learn how authenticating to the Vela API works.
---

## Overview

Authentication for the Vela API is the responsibility of the client initiating the request.

Each request requires a token to be provided as an `Authorization` HTTP header.

The content of this header should be using the `Bearer <token>` scheme.

```sh
Authorization: Bearer <token>
```

{{% alert color="info" %}}
For more information, you can visit the [Swagger authentication documentation](https://swagger.io/docs/specification/authentication/bearer-authentication/).
{{% /alert %}}

## Format

Vela tokens are based off the format of the [JSON Web Token](https://jwt.io/) (a.k.a. JWT) standard.

The token can be broken down into 3 distinct sections, separated by periods (`.`):

* **Header** - metadata about the type of token and the signing algorithm used
* **Payload** - data (a.k.a. claims) providing additional information
* **Signature** - encoded string based off the header, payload and secret

```sh
# syntax
header.payload.signature

# sample
xxxxx.yyyyy.zzzzz
```

{{% alert color="info" %}}
For more information, you can visit the [JWT introduction documentation](https://jwt.io/introduction/).
{{% /alert %}}

## Sample

```sh
curl \
  -X GET \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/users"
```
