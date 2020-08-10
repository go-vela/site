---
title: "Key"
linkTitle: "Key"
description: >
  This section contains information on the key component for a secret.
---

The `key` component is a part of a [secret](/docs/concepts/pipeline/secrets/) for Vela.

This declaration allows you to provide the path to the secret to fetch from the storage backend.

{{% alert color="info" %}}
This component inherits a default value from the secret `name`.
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
+   key: github/octocat/username
    type: repo

  - name: password
    engine: native
+   key: github/octocat/password
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

- `username`
- `password`

This pipeline will also add the following environment variables to the `test` step:

- `USERNAME=<value>`
- `PASSWORD=<value>`
  {{% /alert %}}
