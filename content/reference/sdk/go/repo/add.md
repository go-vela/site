---
title: 'Add'
linkTitle: 'Add'
description: >
  Learn how to create a repo.
---

## Function

```go
func (svc *RepoService) Add(r *library.Repo) (*library.Repo, *Response, error)
```

{{% alert color="info" %}}
For more information, you can view our [go documentation](https://godoc.org/github.com/go-vela/sdk-go/vela#RepoService.Add).
{{% /alert %}}

## Parameters

The following parameters are used to configure the function:

| Name | Description         |
| ---- | ------------------- |
| `r`  | information on repo |

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

You can find an example of this function [here](https://godoc.org/github.com/go-vela/sdk-go/vela#example-RepoService-Add).
