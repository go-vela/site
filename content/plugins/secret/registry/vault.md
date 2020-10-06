---
title: "Vault"
linkTitle: "Vault"
description: >
  Learn about the Vault secret plugin.
---

## Overview

This plugin enables the ability pull secrets from [Vault](https://www.vaultproject.io/) into the secret mount within a Vela pipeline.

Source Code: https://github.com/go-vela/secret-vault

Registry: https://hub.docker.com/r/target/secret-vault

## Usage

{{% alert color="warning" %}}
Users should refrain from using `latest` as the tag for the Docker image.

It is recommended to use a semantically versioned tag instead.
{{% /alert %}}

Sample of writing a secret using token authentication:

```yaml
secrets:
  - origin:
      name: vault
      image: target/vela/secret-vault:latest
      pull: always
      parameters:
        addr: vault.company.com
        token: superSecretVaultToken
        auth_method: token
        items:
          # Written to path: "/vela/secrets/docker/<key>"
          - source: secret/vela/username
            path: docker
```

Sample of reading a secret using ldap authentication:

```diff
secrets:
  - origin:
      name: vault
      image: target/vela/secret-vault:latest
      pull: always
      parameters:
        addr: vault.company.com
+       username: octocat
+       password: superSecretPassword
-       token: superSecretVaultToken
+       auth_method: ldap
        items:
          # Written to path: "/vela/secrets/docker/<key>"
          - source: secret/vela/username
            path: docker
```

Sample of reading a secret using ldap authentication with verbose logging:

```diff
secrets:
  - origin:
      name: vault
      image: target/vela/secret-vault:latest
      pull: always
      parameters:
        addr: vault.company.com
        username: octocat
        password: superSecretPassword
        token: superSecretVaultToken
        auth_method: ldap
+       log_level: trace        
        items:
          # Written to path: "/vela/secrets/docker/<key>"
          - source: secret/vela/username
            path: docker
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.

Secrets used within the secret plugin must exist as Vela secrets.
{{% /alert %}}

Users can use [Vela internal secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
secrets:
  # Repo secret created within Vela
  - name: vault_token
  
  # Example using token authentication method
  - origin:
      name: vault
      image: target/vela/secret-vault:latest
      pull: always
+     secret: [ vault_token ]
      parameters:
        addr: vault.company.com
-       token: superSecretVaultToken
        auth_method: token
        items:
          # Written to path: "/vela/secrets/docker/<key>"
          - source: secret/vela/username
            path: docker
```

{{% alert color="info" %}}
This example will add the `secrets` to the `vault` step as environment variables:

- `VAULT_TOKEN=<value>`
{{% /alert %}}

## Parameters

The following parameters are used to configure the image:

| Name          | Description                                              | Required  | Default |
| ------------- | -------------------------------------------------------- | --------- | ------- |
| `addr`        | address to the instance                                  | `true`    | `N/A`   |
| `auth_method` | authentication method for interfacing (i.e. token, ldap) | `true`    | `N/A`   |
| `log_level`   | set the log level for the plugin                         | `true`    | `info`  |
| `password`    | password for server authentication with ldap             | `false`   | `N/A`   |
| `token`       | token for server authentication                          | `false`   | `N/A`   |
| `username`    | set the log level for the plugin                         | `false`   | `N/A`   |

#### Read

The following parameters are used to configure reading:

| Name    | Description                                      | Required | Default |
| ------- | ------------------------------------------------ | -------- | ------- |
| `items` | enables pretending to perform the apply          | `true`  | `false` |

## Template

COMING SOON!

## Troubleshooting

You can start troubleshooting this plugin by tuning the level of logs being displayed:

```diff
secrets:
  - origin:
      name: vault
      image: target/vela/secret-vault:latest
      pull: always
      parameters:
+       log_level: trace
        addr: vault.company.com
        token: superSecretVaultToken
        auth_method: token
        items:
          # Written to path: "/vela/secrets/docker/<key>"
          - source: secret/vela/username
            path: docker
```

Below are a list of common problems and how to solve them:

COMING SOON!
