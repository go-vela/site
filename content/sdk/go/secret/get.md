---
title: "Get"
linkTitle: "Get"
description: >
  Learn how to list secrets.
---

## Function

```go
func (svc *SecretService) GetAll(engine, sType, org, name string, opt *ListOptions) (*[]library.Secret, *Response, error)
```

{{% alert color="info" %}}
For more information, you can view our [go documentation](https://godoc.org/github.com/go-vela/sdk-go/vela#SecretService.GetAll).
{{% /alert %}}

## Parameters

The following parameters are used to configure the function:

| Name     | Description                |
| -------- | -------------------------- |
| `engine` | name of engine for secret  |
| `sType`  | name of type of secret     |
| `org`    | name of organization       |
| `name`   | name of repository or team |
| `opt`    | options for listing builds |

## Permissions

COMING SOON!

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate with the SDK.

To authenticate with the SDK, please review the [authentication documentation](/docs/sdk/authentication/).
{{% /alert %}}

You can find an example of this function [here](https://godoc.org/github.com/go-vela/sdk-go/vela#example-SecretService-GetAll).
