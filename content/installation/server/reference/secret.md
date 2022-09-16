---
title: "Secret"
linkTitle: "Secret"
description: >
  This section contains information on the secret component for the Vela server.
---

This component is optional and is responsible for integrating with an external secret system based off the configuration provided.

The secret system is used by Vela for storing sensitive application [data at rest](https://en.wikipedia.org/wiki/Data_at_rest).

By default, Vela will use [the database](/docs/installation/server/database/) to store the sensitive data if no other secret system is configured.

{{% alert title="Note:" color="primary" %}}
Any sensitive data stored in the database will be encrypted using the [Advanced Encryption Standard (AES)](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard).
{{% /alert %}}

## Configuration

The following options are used to configure the component:

| Name                       | Description                                                                  | Required | Default | Environment Variables                                         |
| -------------------------- | ---------------------------------------------------------------------------- | -------- | ------- | ------------------------------------------------------------- |
| `secret.vault.addr`        | fully qualified url to the HashiCorp Vault instance                          | `true`   | `N/A`   | `SECRET_VAULT_ADDR`<br>`VELA_SECRET_VAULT_ADDR`               |
| `secret.vault.auth-method` | authentication method used to obtain token from the HashiCorp Vault instance | `false`  | `N/A`   | `SECRET_VAULT_AUTH_METHOD`<br>`VELA_SECRET_VAULT_AUTH_METHOD` |
| `secret.vault.aws-role`    | HashiCorp Vault role used to connect to the auth/aws/login endpoint          | `false`  | `N/A`   | `SECRET_VAULT_AWS_ROLE`<br>`VELA_SECRET_VAULT_AWS_ROLE`       |
| `secret.vault.driver`      | enables HashiCorp Vault as a secret engine                                   | `true`   | `false` | `SECRET_VAULT`<br>`VELA_SECRET_VAULT`                         |
| `secret.vault.prefix`      | prefix for k/v secrets in the HashiCorp Vault instance                       | `false`  | `N/A`   | `SECRET_VAULT_PREFIX`<br>`VELA_SECRET_VAULT_PREFIX`           |
| `secret.vault.renewal`     | frequency to renew the token for the HashiCorp Vault instance                | `false`  | `30m`   | `SECRET_VAULT_RENEWAL`<br>`VELA_SECRET_VAULT_RENEWAL`         |
| `secret.vault.token`       | token required to access the HashiCorp Vault instance                        | `true`   | `N/A`   | `SECRET_VAULT_TOKEN`<br>`VELA_SECRET_VAULT_TOKEN`             |
| `secret.vault.version`     | version for the k/v backend for the HashiCorp Vault instance                 | `true`   | `2`     | `SECRET_VAULT_VERSION`<br>`VELA_SECRET_VAULT_VERSION`         |

{{% alert title="Note:" color="primary" %}}
For more information on these configuration options, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}

## Drivers

The following drivers are available to configure the component:

| Name    | Description                                                        | Documentation                |
| ------- | ------------------------------------------------------------------ | ---------------------------- |
| `vault` | uses a HashiCorp Vault instance for storing sensitive data at rest | https://www.vaultproject.io/ |

### HashiCorp Vault

From the [HashiCorp Vault official website](https://www.vaultproject.io/):

> HashiCorp Vault enables you to secure, store and tightly control access to tokens, passwords, certificates, encryption keys for protecting secrets and other sensitive data using a UI, CLI, or HTTP API.

The below configuration displays an example of starting the Vela server that will connect to a HashiCorp Vault instance:

```diff
$ docker run \
  --detach=true \
  --env=VELA_ADDR=https://vela-server.example.com \
  --env=VELA_DATABASE_ENCRYPTION_KEY=<encryption-key> \
  --env=VELA_QUEUE_DRIVER=redis \
  --env=VELA_QUEUE_ADDR=redis://<password>@<hostname>:<port>/<database> \
  --env=VELA_PORT=443 \
  --env=VELA_SECRET=<shared-secret> \
+ --env=VELA_SECRET_VAULT=true \
+ --env=VELA_SECRET_VAULT_ADDR=https://vault.example.com \
+ --env=VELA_SECRET_VAULT_TOKEN=<vault-token>
  --env=VELA_SCM_CLIENT=<oauth-client-id> \
  --env=VELA_SCM_SECRET=<oauth-client-secret> \
  --env=VELA_WEBUI_ADDR=https://vela.example.com \
  --name=server \
  --publish=80:80 \
  --publish=443:443 \
  --restart=always \
  target/vela-server:latest
```