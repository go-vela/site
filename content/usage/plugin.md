---
title: "Working with plugins"
toc: true
description: >
  Walkthrough of an example using pipeline and secret plugins working together
---

{{% alert title="Note:" color="primary" %}}
The following plugins are used within the example

* [Kaniko](/docs/plugins/registry/pipeline/kaniko/)
* [Vault](/docs/plugins/registry/secret/vault/)
{{% /alert %}}

Typically, plugins are configured as a step in a pipeline and should accept their configuration via environment variables. The below example shows a pipeline and secret plugin working together to publish an image to a registry:

```yaml
version: "1"

steps:
  - name: plugin
    image: target/vela-docker
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world

secrets:
  - name: vault_token
    key: go-vela/vault_token
    engine: native
    type: org

  - origin:
      name: plugin
      image: target/secret-vault
      pull: always
      secrets: [ vault_token ]
      parameters:
        addr: vault.company.com
        auth_method: token
        items:
          - source: secret/docker
            path: docker
```

We pass these variables in Vela using the `parameters` block. Any variable passed to this block, will be injected into the step as `PARAMETER_<variable>`:

```diff
version: "1"

steps:
  - name: docker
    image: target/vela-docker
    pull: always
+   parameters:
+     registry: index.docker.io
+     repo: index.docker.io/octocat/hello-world

secrets:
  - name: vault_token
    key: go-vela/vault_token
    engine: native
    type: org

  - origin:
      name: vault
      image: target/secret-vault
      pull: always
      secrets: [ vault_token ]
+     parameters:
+       addr: vault.company.com
+       auth_method: token
+       items:
+         - source: secret/docker
+           path: docker
```

From the above example, the following environment variables would be added to the containers:

**Docker:**

* `PARAMETER_REGISTRY=index.docker.io`
* `PARAMETER_REPO=index.docker.io/octocat/hello-world`

**Vault:**

* `PARAMETER_ADDR=index.docker.io`
* `PARAMETER_AUTH_METHOD=index.docker.io/octocat/hello-world`
* `PARAMETER_ITEMS={"items": [{"source": "secret/docker"}],"path": "docker"}`
