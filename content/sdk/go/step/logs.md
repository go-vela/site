---
title: "Logs"
linkTitle: "Logs"
description: >
  Learn how to view logs for a step.
---

## Function

```go
func (svc *LogService) GetStep(org, repo string, build, step int) (*library.Log, *Response, error)
```

{{% alert color="info" %}}
For more information, you can view our [go documentation](https://godoc.org/github.com/go-vela/sdk-go/vela#LogService.GetStep).
{{% /alert %}}

## Parameters

The following parameters are used to configure the endpoint:

| Name    | Description          |
| ------- | -------------------- |
| `org`   | name of organization |
| `repo`  | name of repository   |
| `build` | number of build      |
| `step`  | number of step       |

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

You can find an example of this function [here](https://godoc.org/github.com/go-vela/sdk-go/vela#example-LogService-GetStep).
