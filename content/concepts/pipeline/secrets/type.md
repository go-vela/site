---
title: "Type"
linkTitle: "Type"
description: >
  This section contains information on the type component for a secret.
---

The `type` component is a part of a [secret](/docs/concepts/pipeline/secrets/) for Vela.

This declaration allows you to provide the type of secret to fetch from the storage backend.

{{% alert color="info" %}}
This component has a default value of `repo`.
{{% /alert %}}

## Options

The following options are available to configure the component:

| Name     | Description                                             |
| -------- | ------------------------------------------------------- |
| `org`    | secret scoped to any repository in an organization      |
| `repo`   | secret scoped to a single repository in an organization |
| `shared` | secret scoped to any repository in the installation     |

#### Org

Secrets with an `org` type are accessible by any repository in an organization.

{{% alert color="info" %}}
This secret type requires you to have `admin` access to the organization.
{{% /alert %}}

#### Repo

Secrets with a `repo` type are accessible by a single repository in an organization.

{{% alert color="info" %}}
This secret type requires you to have `admin` access to the repository.
{{% /alert %}}

#### Shared

Secrets with a `shared` type are accessible by any repository in the Vela installation.

These secrets are unique, because they require a team to exist in your organization.

{{% alert color="info" %}}
This secret type requires you to be a member of the team in the organization.
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

secrets:
  - name: username
    engine: native
    key: example-org/example-repo/username
+   type: repo

  - name: password
    engine: native
    key: example-org/example-repo/password
+   type: repo

steps:
  - name: test
    image: golang
    secrets: [ username, password ]
    commands:
      - echo "machine github.com" > .netrc
      - echo "login ${USERNAME}" > .netrc
      - echo "password ${PASSWORD}" > .netrc
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will allow the following secrets to be referenced:

- `username`
- `password`

This pipeline will also add the following environment variables to the `test` step:

- `USERNAME=<value>`
- `PASSWORD=<value>`
  {{% /alert %}}
