---
title: "Secret"
linkTitle: "Secret"
description: >
  Learn about secret plugins for Vela.
---

## Under the hood

Secret plugins are designed to be used to read secrets in volumes within the Vela workspace. When a secret plugin runs the plugin should write data to the custom Vela mount (`/vela/secrets/`) as key/value pairs. 

```diff
secrets:
  - name: vault_token

  - origin:
      name: vault
      image: target/secret-vault
      pull: true
      secrets: [ vault_token ]
+     parameters:
+       addr: vault.company.com
+       auth_method: token
+       username: octocat
+       items:
+         - source: secret/docker
+           path: docker  
```

From the above example, will have written the following available secrets to:

* `/vela/secrets/docker/<key>/<value/`

## Building a plugin

The reason we use the environment for configuration is because it allows plugins to be written in any language! We have a number of tutorials that can help you get started in writing a plugin in your preferred language.

Before you get started writing a plugin you should have a good understanding of how Docker images are built. This will allow you to build a optimal plugin that follows [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).

{{% alert color="tip" %}}
We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

**All** secret plugins should write secret data to the `/vela/secrets/` workspace. This ensures that secrets read into the pipeline are compatible with pipeline plugins.
