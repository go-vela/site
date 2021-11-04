---
title: "Origin"
linkTitle: "Origin"
description: >
  This section contains information on the origin component for a secret.
---

The `origin` component is a part of a [secret](/docs/tour/secrets/) for Vela.

This declaration allows you to pull secrets from non-internal secret providers via plugins.

{{% alert color="info" %}}
To see what plugins are supported and how they integrate with the Vela build lifecycle see the [plugins page](/docs/plugins/registry/secret/)
{{% /alert %}}

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

secrets:
  # Implicit secret definition.
  - name: vault_token

+  - origin:
+     name: vault external secrets
+     image: target/secret-vault
+     secrets: [ vault_token ]
+     parameters:
+       addr: vault.company.com
+       auth_method: token
+       username: octocat
+       items:
+         - source: secret/vela
+           path: user

steps:
  - name: test
    image: golang
    secrets: [ username, password ]
    commands:
      - cat /vela/secrets/user/name
      - cat /vela/secrets/user/password
```

{{% alert color="info" %}}
To see more information on the Vault plugin usage see the [Vault docs](/docs/plugins/registry/secret/vault)
{{% /alert %}}
