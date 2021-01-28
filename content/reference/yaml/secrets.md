---
title: "Secrets"
linkTitle: "Secrets"
weight: 8
description: >
  YAML tags for secret block
---

The secret tag is intended to be used to pull secrets from the Vela server or execute 
plugins to write the external secrets to the build volume.

```yaml
---
# This document is displaying all the required tags
# to pull various secret types. 
secrets: 
  # Below is displaying the implicit native secret definition. This definition 
  # is only supported for native secrets of repository type.
  - name: foo

  # Below is displaying the declarative secret definitions.
  - name: foo1
    key: go-vela/docs/foo1
    engine: native
    type: repo
  - name: foo2
    key: go-vela/foo2`
    engine: native
    type: org
  - name: foo3
    key: go-vela/admins/foo3
    engine: native
    type: shared

  # Below is displaying executing a secret plugin.
  - origin:
     name: External Vault Secret
     image: target/secret-vault:latest
     parameters:
       addr: vault.company.com
       auth_method: token
       username: vela
       token: sometoken
       items:
         - source: secret/vela
           path: user    
```

## Tags

| Tag     | Required | Type   | Description                                                     |
|---------|----------|--------|-----------------------------------------------------------------|
| `name`  | Y        | string | Name of secret to reference in the pipeline.                    |
| `key`   | N        | string | Path to secret to fetch from storage backend.                   |
| `engine`| N        | string | Name of storage backend to fetch secret from.                   |
| `type`  | N        | string | Type of secret to fetch from storage backend.                   |
| `origin`| N        | struct | Declaration to pull secrets from non-internal secret providers. |

#### The `name:` tag

```yaml
---
secrets: 
    # Name of secret to reference in the pipeline.
  - name: postgres
```

#### The `key:` tag

{{% alert title="Tip:" color="info" %}}
The key is unique
    # to the type of secret you need to pull and follows a pattern
    # to ensure the repo has the proper authorization to use the secret.
    # Pattern by type:
    # repo    - <org>/<repo>/<some_name>
    # org     - <org>/<some_name>
    # shared  - <org>/<team_with_org>/<some_name>
{{% /alert %}}

```yaml
---
secrets: 
    # Path to secret to fetch from storage backend. Displaying a 
    # repo type secret. 
  - key: go-vela/docs/foo1

    # Path to secret to fetch from storage backend. Displaying a 
    # org type secret.
  - key: go-vela/foo1
  
    # Path to secret to fetch from storage backend. Displaying a 
    # shared type secret.
  - key: go-vela/admins/foo1  
```

#### The `engine:` tag

{{% alert title="Tip:" color="info" %}}
To know what engines are available for your Vela installation, we recommend consulting your system administrators.
{{% /alert %}}

```yaml
---
secrets: 
    # Name of storage backend to fetch secret from, "native" signifies
    # the backend provide it the Vela database. 
  - engine: native
```

#### The `type:` tag

```yaml
---
secrets: 
    # Type of secret to fetch from storage backend.
    # By default, Vela can pull repo but tag accepts the 
    # following values: repo, org, and shared
  - type: repo
```

#### The `origin:` tag

| Tag           | Required | Type            | Description                                                      |
|---------------|----------|-----------------|------------------------------------------------------------------|
| `name`        | Y        | string          | Unique identifier for the container in the pipeline.             |
| `image`       | Y        | []string        | Docker image used to create an ephemeral container.                 |
| `pull`        | N        | string          | Declaration to configure if and when the Docker image is pulled. |
| `secrets`     | N        | struct          | Sensitive variables injected into the container environment.     |
| `environment` | N        | map || []string | Variables to inject into the container environment.              |
| `ruleset`     | N        | struct          | Conditions to limit the execution of the container.              |
| `parameters`  | N        | map             | Extra configuration variables specific to a plugin.              |

{{% alert title="Tip:" color="info" %}}
In an effort to reduce duplicate documentation, see the comparable [step tags documentation](/docs/reference/yaml/steps/#tags) to learn how tags can be set and details on behavior.
{{% /alert %}}