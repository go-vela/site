---
title: "Engine"
linkTitle: "Engine"
description: >
  This section contains information on the engine component for a secret.
---

The `engine` component is a part of a [secret](/docs/concepts/pipeline/secrets) for Vela.

This declaration allows you to provide the name of the storage backend to fetch the secret from.

{{% alert color="info" %}}
This component has a default value of `native`.
{{% /alert %}}

## Options

The following options are available to configure the component:

| Name     | Description                                        |
| -------- | -------------------------------------------------- |
| `native` | uses the Vela database for secret storage          |
| `vault`  | uses a HashiCorp Vault instance for secret storage |

#### Native

The `native` secret engine is designed to store secrets in the Vela database.

#### Vault

The `vault` secret engine is designed to store secrets in a [HashiCorp Vault](https://www.vaultproject.io/) instance.

For secret storage information refer to [Vault's documentation](https://www.vaultproject.io/docs/).

{{% alert color="warning" %}}
Vault is currently not supported. Using Vault is coming soon!
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

secrets:
  - name: username
+    engine: native
    key: username
    type: repo

  - name: password
+    engine: native
    key: password
    type: repo

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
* `username`
* `password`

This pipeline will also add the following environment variables to the `test` step:
* `USERNAME=<value>`
* `PASSWORD=<value>`
{{% /alert %}}
