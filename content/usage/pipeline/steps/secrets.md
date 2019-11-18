---
title:  "Secrets"
toc:  true
weight:  9
description: >
  Set secrets that can be used within your build step.
---

The `secrets` declaration for a pipeline instructs Vela what secrets to retrieve before executing a build.

```diff
version: "1"

+secrets:
+  - name: docker_username
+    key:  docker_username
+    engine: native
+    type: repo
+  - name: docker_password
+    key:  docker_password
+    engine: native
+    type: repo
```

This top level declaration then allows injection of these secret variables into the environment for the provided build step(s). The step(s) request access to these variables using the same `secrets` declaration which injects the variables into the runtime environment as all upper case variables.

```diff
version: "1"

steps:
  - name: docker
-   username: <username>
-   password: <password>
+   secrets: [ docker_username, docker_password ]

secrets:
  - name: docker_username
    key:  docker_username
    engine: native
    type: repo
  - name: docker_password
    key:  docker_password
    engine: native
    type: repo
```

### Alternate Names

There may be scenarios where there is a requirement to store secrets using alternate names. Secrets can be mapped to an alternate name when injected into the entire build or an individual build step.

```diff
version: "1"

steps:
  - name: docker
-   secrets: [ docker_username, docker_password ]
+   secrets:
+     - source: docker_eng_username
+       target: docker_username
+     - source: docker_eng_password
+       target: docker_password

+secrets:
-  - name: docker_username
+  - name: docker_eng_username
+    key:  username
-  - name: docker_password
+  - name: docker_eng_password
+    key:  password
```

### Reference Secret

Vela offers a number of different ways to reference your secrets. To see the full set of options navigate to the [secret reference](/usage/reference/pipeline/secret/) section.
