---
title: "Sync"
linkTitle: "Sync"
description: >
  Learn how to sync a repo with SCM.
---

## Endpoint

```
PATCH  /api/v1/scm/repos/:org/:repo/sync
```

## Parameters

The following parameters are used to configure the endpoint:

| Name   | Description          |
| ------ | -------------------- |
| `org`  | name of organization |
| `repo` | name of repository   |

## Responses

| Status Code | Description                                         |
| ----------- | --------------------------------------------------- |
| `200`       | indicates the request has succeeded                 |
| `401`       | indicates the user does not have proper permissions |

## Description

The sync endpoint allows users to re-align their repository in Vela with its SCM mirror. This discrepancy can come in the form of a repository that has been deleted from the SCM but not in Vela. 

Further, as of `v0.19.0`, the sync endpoint can be used to adjust events that are sent to Vela from the SCM that the Vela-instance of the repo is not subscribed to. For example, if your audit page has errors like

```sh
"unable to process webhook: <org>/<repo> does not have comment events enabled"
```

hitting the sync endpoint should re-configure the SCM webhook to only send events that are allowed. Once aligned, you should not have to hit this endpoint again, even if the subscribed events are changed.

## Sample

{{% alert color="warning" %}}
This section assumes you already know how to authenticate to the API.

To authenticate to the API, please review the [authentication documentation](/docs/reference/api/authentication/).
{{% /alert %}}

#### Request

```sh
curl \
  -X PATCH \
  -H "Authorization: Bearer <token>" \
  "http://127.0.0.1:8080/api/v1/scm/repos/github/octocat/sync"
```

#### Response

```sh
repo "github/octocat" synced
```