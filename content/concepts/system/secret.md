---
title: "Secret"
linkTitle: "Secret"
description: >
  This section contains information on the secret component in the system.
---

The `secret` component is part of the core system components for Vela.

A `secret` is defined as a piece of sensitive data or information that you want to tightly control access to. These are extremely useful when trying to avoid providing the data in plain text. They typically include

{{% alert color="info" %}}
The following list are some examples of secrets:

- API keys
- certificates
- passwords
- tokens
- much, much more...
  {{% /alert %}}

## Fields

The following fields make up this component:

| Name            | Type       | Description                                             |
| --------------- | ---------- | ------------------------------------------------------- |
| `allow_command` | `bool`     | enable injecting a secret with a `commands` declaration |
| `events`        | `[]string` | list of events permitted to access the secret           |
| `id`            | `int64`    | unique identifier for secret in the system              |
| `images`        | `[]string` | list of images permitted to access the secret           |
| `name`          | `string`   | unique name of the secret                               |
| `org`           | `string`   | unique org from source control provider                 |
| `repo`          | `string`   | unique repo name in org from source control provider    |
| `team`          | `string`   | unique team name in org from source control provider    |
| `type`          | `string`   | type of secret to store in the storage backend          |
| `value`         | `string`   | sensitive data or information stored in the backend     |

{{% alert color="info" %}}
This component is stored in the configured Vela backend in the `secrets` table.
{{% /alert %}}

#### Types

The following types are available to configure the component:

| Name     | Description                                             |
| -------- | ------------------------------------------------------- |
| `org`    | secret scoped to any repository in an organization      |
| `repo`   | secret scoped to a single repository in an organization |
| `shared` | secret scoped to any repository in the installation     |

###### Org

Secrets with an `org` type are accessible by any repository in an organization.

{{% alert color="info" %}}
This secret type requires you to have `admin` access to the organization.
{{% /alert %}}

###### Repo

Secrets with a `repo` type are accessible by a single repository in an organization.

{{% alert color="info" %}}
This secret type requires you to have `admin` access to the repository.
{{% /alert %}}

###### Shared

Secrets with a `shared` type are accessible by any repository in the Vela installation.

These secrets are unique, because they require a team to exist in your organization.

{{% alert color="info" %}}
This secret type requires you to be a member of the team in the organization.
{{% /alert %}}

## References

- [API](/docs/api/secret/)
- [CLI](/docs/cli/secret/)
- SDK
  - [Go](/docs/sdk/go/secret/)
