---
title: "Secret"
linkTitle: "Secret"
description: >
  This section contains information on the secret server component.
---

The `secret` component is one of the server components for Vela.

This component defines the system Vela uses for storing and accessing [secrets](/docs/concepts/system/secret).

## Configuration

The following options are used to configure the component:

| Name           | Environment          | Description                                   |
| -------------- | -------------------- | --------------------------------------------- |
| `vault.driver` | `SECRET_VAULT`       | enables the Vault secret engine               |
| `vault.addr`   | `SECRET_VAULT_ADDR`  | full navigatable url to Vault installation    |
| `vault.token`  | `SECRET_VAULT_TOKEN` | token required to read/write secrets to Vault |

{{% alert color="info" %}}
All available options support `VELA_*` prefixes for the environment variables. For example:
* `SECRET_VAULT` - enables the Vault secret engine
* `VELA_SECRET_VAULT` - enables the Vault secret engine
{{% /alert %}}
