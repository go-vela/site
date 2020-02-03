---
title: "Environment"
linkTitle: "Environment"
description: >
  This section contains information on the environment component for a service.
---

The `environment` component is a part of a [service](/docs/usage/concepts/pipeline/services) for Vela.

This declaration allows you to provide variables injected into the container environment.

## Syntax

The following is an example of valid syntax for the component:

```diff
version: "1"

metadata:
  template: false

services:
  - name: postgres
    image: postgres:12
+    environment:
+      POSTGRES_DB: example
+      POSTGRES_USER: example

steps:
  - name: test
    image: golang
    environment:
      DATABASE_DRIVER: postgres
      DATABASE_CONFIG: 'postgres://example@postgres:5432/example?sslmode=disable'
    commands:
      - go test ./...
```

{{% alert color="info" %}}
This pipeline will start the `postgres` service first, then run the `test` step.
{{% /alert %}}

## Defaults

The following environment variables are injected into every service:

#### Build Environment Variables

| Key                  | Value                                                                                    | Explanation                                                         |
| ---------------------| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `BUILD_AUTHOR`       | `octocat`                                                                                | author from the source commit                                       |
| `BUILD_AUTHOR_EMAIL` | `octocat@github.com`                                                                     | author email from the source commit                                 |
| `BUILD_BRANCH`       | `master`                                                                                 | branch from the source commit                                       |
| `BUILD_CHANNEL`      | `vela`                                                                                   | queue channel the build was published to                            |
| `BUILD_COMMIT`       | `7fd1a60b01f91b314f59955a4e4d4e80d8edf11d`                                               | commit sha from the source commit                                   |
| `BUILD_CREATED`      | `1556720958`                                                                             | unix timestamp representing build creation time                     |
| `BUILD_ENQUEUED`     | `1556730001`                                                                             | unix timestamp representing build enqueue time                      |
| `BUILD_EVENT`        | `push`                                                                                   | webhook event that triggered the build                              |
| `BUILD_FINISHED`     | `1556730045`                                                                             | unix timestamp representing build completion time                   |
| `BUILD_HOST`         | `vela-worker-1`                                                                          | fully qualified domain name of the worker the build was executed on |
| `BUILD_LINK`         | `https://vela-server.localhost/octocat/hello-world/1`                                    | link to the build in the UI                                         |
| `BUILD_MESSAGE`      | `New line at end of file.`                                                               | message from the source commit                                      |
| `BUILD_NUMBER`       | `1`                                                                                      | build number                                                        |
| `BUILD_PARENT`       | `1`                                                                                      | previous build number                                               |
| `BUILD_REF`          | `refs/heads/master`                                                                      | reference from the source commit                                    |
| `BUILD_STARTED`      | `1556730001`                                                                             | unix timestamp representing build start time                        |
| `BUILD_SOURCE`       | `https://github.com/octocat/hello-world/commit/7fd1a60b01f91b314f59955a4e4d4e80d8edf11d` | link from the source commit                                         |
| `BUILD_TITLE`        | `Merge pull request #6 from octocat/patch-1`                                             | title from the source commit                                        |
| `BUILD_WORKSPACE`    | `/home/octocat_hello-world_1`                                                            | working directory the build is executed in                          |
| `BUILD_TAG`          | `v1.0.0`                                                                                 | tag is populated from the source reference                          |

{{% alert color="info" %}}
* `BUILD_LINK` is not populated if the Vela server is configured to run headless (no UI).
* `BUILD_TAG` is only populated during `tag` events.
{{% /alert %}}

#### Vela Environment Variables

| Key              | Value                         | Explanation                                                         |
| ---------------- | ----------------------------- | ------------------------------------------------------------------- |
| `VELA`           | `true`                        | environment is Vela                                                 |
| `VELA_ADDR`      | `vela-server.localhost`       | fully qualified domain name of the Vela server                      |
| `VELA_CHANNEL`   | `vela`                        | queue channel the build was published to                            |
| `VELA_DATABASE`  | `postgres`                    | database Vela is connected to                                       |
| `VELA_HOST`      | `vela-worker-1`               | fully qualified domain name of the worker the build was executed on |
| `VELA_QUEUE`     | `redis`                       | queue build was published to                                        |
| `VELA_RUNTIME`   | `docker`                      | runtime environment build was executed in                           |
| `VELA_SOURCE`    | `github`                      | queue channel the build was published to                            |
| `VELA_VERSION`   | `v0.1.0`                      | Vela version                                                        |
| `VELA_WORKSPACE` | `/home/octocat_hello-world_1` | working directory the build is executed in                          |
| `CI`             | `vela`                        | CI enabled is Vela                                                  |

#### Repository Environment Variables

| Key                    | Value                                        | Explanation                        |
| ---------------------- | -------------------------------------------- | ---------------------------------- |
| `REPOSITORY_BRANCH`    | `master`                                     | default branch of the repository   |
| `REPOSITORY_CLONE`     | `https://github.com/octocat/hello-world.git` | clone url of the repository        |
| `REPOSITORY_FULL_NAME` | `octocat/hello-world`                        | full name of the repository        |
| `REPOSITORY_LINK`      | `https://github.com/octocat/hello-world`     | direct url of the repository       |
| `REPOSITORY_NAME`      | `hello-world`                                | name of the repository             |
| `REPOSITORY_ORG`       | `octocat`                                    | org of the repository              |
| `REPOSITORY_PRIVATE`   | `false`                                      | privacy setting for the repository |
| `REPOSITORY_TIMEOUT`   | `60`                                         | timeout setting for the repository |
| `REPOSITORY_TRUSTED`   | `false`                                      | trusted setting for the repository |
