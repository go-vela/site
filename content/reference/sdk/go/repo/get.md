---
title: 'Get'
linkTitle: 'Get'
description: >
  Learn how to list repos.
---

## Function

```go
func (svc *RepoService) GetAll(opt *ListOptions) (*[]library.Repo, *Response, error)
```

{{% alert color="info" %}}
For more information, you can view our [go documentation](https://godoc.org/github.com/go-vela/sdk-go/vela#RepoService.GetAll).
{{% /alert %}}

## Parameters

The following parameters are used to configure the function:

| Name  | Description               |
| ----- | ------------------------- |
| `opt` | options for listing repos |

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

To authenticate with the SDK, please review the [authentication documentation](/docs/sdk/go/authentication/).
{{% /alert %}}

You can find an example of this function [here](https://godoc.org/github.com/go-vela/sdk-go/vela#example-RepoService-GetAll).
