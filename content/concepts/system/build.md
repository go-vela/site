---
title: "Build"
linkTitle: "Build"
description: >
  This section contains information on the build component in the system.
---

The `build` component is part of the core system components for Vela.

A `build` is defined as a single, ephemeral execution of a [pipeline](/docs/concepts/pipeline/).

A build is comprised of one or many [services](/docs/concepts/system/service/) and [steps](/docs/concepts/system/step/) that contain the instructions to execute from the pipeline.

{{% alert color="info" %}}
A build is typically created from a [hook](/docs/concepts/system/hook/) triggered by a [repo](/docs/concepts/system/repo/) in the source control provider.
{{% /alert %}}

## Fields

The following fields make up this component:

| Name           | Type     | Description                                                  |
| -------------- | -------- | ------------------------------------------------------------ |
| `author`       | `string` | author from the commit that triggered the build              |
| `branch`       | `string` | branch from the commit that triggered the build              |
| `base_ref`     | `string` | sha from the commit that triggered the build                 |
| `clone`        | `string` | full clone url for the repo that triggered the build         |
| `commit`       | `string` | sha from the commit that triggered the build                 |
| `created`      | `int64`  | UNIX timestamp for when the build was created                |
| `deploy`       | `string` | environment targeted for deployment                          |
| `distribution` | `string` | operating system the build was executed on                   |
| `email`        | `string` | email for author from the commit that triggered the build    |
| `enqueued`     | `int64`  | UNIX timestamp for when the build was published to the queue |
| `error`        | `string` | error message received during build execution time           |
| `event`        | `string` | event from the commit that triggered the build               |
| `finished`     | `int64`  | UNIX timestamp for when the build was completed              |
| `host`         | `string` | hostname the build was executed on                           |
| `id`           | `int64`  | unique identifier for build in the system                    |
| `link`         | `string` | full navigatable url to the build in the system              |
| `message`      | `string` | message from the commit that triggered the build             |
| `number`       | `int`    | unique identifier for build triggered from the repo          |
| `parent`       | `int`    | unique identifier for previous build triggered from the repo |
| `ref`          | `string` | reference from the commit that triggered the build           |
| `repo_id`      | `int64`  | unique identifier for repo that triggered the build          |
| `runtime`      | `string` | runtime the build was executed with                          |
| `sender`       | `string` | sender that triggered the build                              |
| `started`      | `int64`  | UNIX timestamp for when the build was started                |
| `status`       | `string` | signifies the end condition for the build                    |
| `source`       | `string` | full url from the commit that triggered the build            |
| `title`        | `string` | title from the commit that triggered the build               |

{{% alert color="info" %}}
This component is stored in the configured Vela backend in the `builds` table.
{{% /alert %}}

## References

- [API](/docs/api/build/)
- [CLI](/docs/cli/build/)
- SDK
  - [Go](/docs/sdk/go/build/)
