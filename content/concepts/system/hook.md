---
title: "Hook"
linkTitle: "Hook"
description: >
  This section contains information on the hook component in the system.
---

The `hook` component is part of the core system components for Vela.

A `hook` is defined as a single, webhook object received from a [repo](/docs/concepts/system/repo) in the source control provider prompting Vela to perform an action.

In most cases, processing a hook involves fetching the [pipeline](/docs/concepts/pipeline) from the repo and triggering a [build](/docs/concepts/system/build).

{{% alert color="info" %}}
From [GitHub's webhook documentation](https://help.github.com/en/github/extending-github/about-webhooks):

> Webhooks provide a way for notifications to be delivered to an external web server whenever certain actions occur on a repository or organization.

{{% /alert %}}

## Fields

The following fields make up this component:

| Name           | Type     | Description                                               |
| -------------- | -------- | --------------------------------------------------------- |
| `branch`       | `string` | branch from the commit that triggered the hook            |
| `build_id`     | `int64`  | unique identifier for build created from the hook         |
| `created`      | `int64`  | UNIX timestamp for when the hook was created              |
| `error`        | `string` | error message received during hook processing             |
| `event`        | `string` | event from the commit that triggered the hook             |
| `host`         | `string` | hostname the hook was received from                       |
| `id`           | `int64`  | unique identifier for hook in the system                  |
| `link`         | `string` | full navigatable url to hook from source control provider |
| `number`       | `int`    | unique identifier for hook triggered from the repo        |
| `repo_id`      | `int64`  | unique identifier for repo that triggered the hook        |
| `status`       | `string` | signifies the end condition for the hook                  |
| `source_id`    | `string` | unique identifier for hook from source control provider   |

{{% alert color="info" %}}
This component is stored in the configured Vela backend in the `hooks` table.
{{% /alert %}}

## References

* [API](/docs/api/build)
* [CLI](/docs/cli/hook)
* SDK
  * [Go](/docs/sdk/go/hook)
