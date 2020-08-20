---
title: "Environment"
linkTitle: "Environment"
description: >
  This section contains information on the environment component for a service.
---

The `environment` component is a part of a [service](/docs/concepts/pipeline/services/) for Vela.

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

| Key                       | Value                                                       | Explanation                                                         |
| ------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------- |
| `VELA_BUILD_AUTHOR`       | `octocat`                                                   | author from the source commit                                       |
| `VELA_BUILD_AUTHOR_EMAIL` | `octocat@github.com`                                        | author email from the source commit                                 |
| `VELA_BUILD_BASE_REF`     | `refs/heads/dev`                                            | reference from the base commit                                      |
| `VELA_BUILD_BRANCH`       | `master`                                                    | branch from the source commit                                       |
| `VELA_BUILD_CHANNEL`      | `vela`                                                      | queue channel the build was published to                            |
| `VELA_BUILD_CLONE`        | `https://github.com/octocat/hello-world.git`                | clone url for the repository the build was triggered from           |
| `VELA_BUILD_COMMIT`       | `7fd1a60b01f91b314f59955a4e4d4e80d8edf11d`                  | commit sha from the source commit                                   |
| `VELA_BUILD_CREATED`      | `1556720958`                                                | unix timestamp representing build creation time                     |
| `VELA_BUILD_DISTRIBUTION` | `linux`                                                     | distribution where the build was executed                           |
| `VELA_BUILD_ENQUEUED`     | `1556720958`                                                | unix timestamp representing build enqueued time                     |
| `VELA_BUILD_EVENT`        | `push`                                                      | webhook event that triggered the build                              |
| `VELA_BUILD_FINISHED`     | `1556730045`                                                | unix timestamp representing build completion time                   |
| `VELA_BUILD_HOST`         | `vela-worker-1`                                             | fully qualified domain name of the worker the build was executed on |
| `VELA_BUILD_LINK`         | `https://vela-server.localhost/octocat/hello-world/1`       | link to the build in the UI                                         |
| `VELA_BUILD_MESSAGE`      | `Merge pull request #6 from octocat/patch-1`                | message from the source commit                                      |
| `VELA_BUILD_NUMBER`       | `1`                                                         | build number                                                        |
| `VELA_BUILD_PARENT`       | `1`                                                         | previous build number                                               |
| `VELA_BUILD_REF`          | `refs/heads/master`                                         | reference from the source commit                                    |
| `VELA_BUILD_RUNTIME`      | `docker`                                                    | runtime where the build was executed                                |
| `VELA_BUILD_SENDER`       | `NealColeman`                                               | user who triggered the build                                        |
| `VELA_BUILD_STARTED`      | `1556730001`                                                | unix timestamp representing build start time                        |
| `VELA_BUILD_STATUS`       | `success`  |                                                | status of the build                                                 |
| `VELA_BUILD_TITLE`        | `push received from https://github.com/octocat/hello-world` | title for the build                                                 |
| `VELA_BUILD_WORKSPACE`    | `/vela/src/github.com/octocat/hello-world`                  | working directory the build is executed in                          |

{{% alert color="info" %}}
The following table includes variables only available during the **comment** event
{{% /alert %}}

| Key                       | Value | Explanation                                                |
| ------------------------- | ----- | ---------------------------------------------------------- |
| `VELA_BUILD_PULL_REQUEST` | `1`   | pull request number is populated from the source reference |
| `VELA_PULL_REQUEST`       | `1`   | pull request number is populated from the source reference |

{{% alert color="info" %}}
The following table includes variables only available during the **deploy** event
{{% /alert %}}

| Key                 | Value        | Explanation                                   |
| ------------------- | -----------  | --------------------------------------------- |
| `VELA_BUILD_TARGET` | `production` | name of target environment for the deployment |
| `VELA_DEPLOYMENT`   | `production` | name of target environment for the deployment |

{{% alert color="info" %}}
The following table includes variables only available during the **pull request** event
{{% /alert %}}

| Key                        | Value    | Explanation                                                |
| -------------------------- | -------- | ---------------------------------------------------------- |
| `VELA_BUILD_PULL_REQUEST`  | `1`      | pull request number is populated from the source reference |
| `VELA_PULL_REQUEST`        | `1`      | pull request number is populated from the source reference |
| `VELA_PULL_REQUEST_SOURCE` | `dev`    | pull request branch from the source reference              |
| `VELA_PULL_REQUEST_TARGET` | `master` | pull request branch for the target reference               |

{{% alert color="info" %}}
The following table includes variables only available during the **tag** event
{{% /alert %}}

| Key              | Value    | Explanation                                |
| ---------------- | -------- | ------------------------------------------ |
| `VELA_BUILD_TAG` | `v1.0.0` | tag is populated from the source reference |


#### Vela Environment Variables

| Key              | Value                                             | Explanation                                                         |
| ---------------- | ------------------------------------------------- | ------------------------------------------------------------------- |
| `VELA`           | `true`                                            | environment is Vela                                                 |
| `VELA_ADDR`      | `vela-server.localhost`                           | fully qualified domain name of the Vela server                      |
| `VELA_CHANNEL`   | `vela`                                            | queue channel the build was published to                            |
| `VELA_DATABASE`  | `postgres`                                        | database Vela is connected to                                       |
| `VELA_HOST`      | `vela-worker-1`                                   | fully qualified domain name of the worker the build was executed on |
| `VELA_QUEUE`     | `redis`                                           | queue build was published to                                        |
| `VELA_RUNTIME`   | `docker`                                          | runtime environment build was executed in                           |
| `VELA_SOURCE`    | `github`                                          | queue channel the build was published to                            |
| `VELA_VERSION`   | `v0.1.0`                                          | Vela version                                                        |
| `VELA_WORKSPACE` | `/vela/src/github.com/github/octocat/hello-world` | working directory the build is executed in                          |
| `CI`             | `vela`                                            | CI enabled is Vela                                                  |

#### Repository Environment Variables

| Key                       | Value                                        | Explanation                                |
| ------------------------- | -------------------------------------------- | ------------------------------------------ |
| `VELA_REPO_ACTIVE`        | `true`                                       | active setting for the repository          |
| `VELA_REPO_ALLOW_COMMENT` | `false`                                      | comment enabled setting for the repository |
| `VELA_REPO_ALLOW_DEPLOY`  | `false`                                      | deploy enabled setting for the repository  |
| `VELA_REPO_ALLOW_PULL`    | `true`                                       | pull enabled setting for the repository    |
| `VELA_REPO_ALLOW_PUSH`    | `true`                                       | push enabled setting for the repository    |
| `VELA_REPO_ALLOW_TAG`     | `false`                                      | tag enabled setting for the repository     |
| `VELA_REPO_BRANCH`        | `master`                                     | default branch of the repository           |
| `VELA_REPO_CLONE`         | `https://github.com/octocat/hello-world.git` | clone url of the repository                |
| `VELA_REPO_FULL_NAME`     | `octocat/hello-world`                        | full name of the repository                |
| `VELA_REPO_LINK`          | `https://github.com/octocat/hello-world`     | direct url of the repository               |
| `VELA_REPO_NAME`          | `hello-world`                                | name of the repository                     |
| `VELA_REPO_ORG`           | `octocat`                                    | org of the repository                      |
| `VELA_REPO_PRIVATE`       | `false`                                      | privacy setting for the repository         |
| `VELA_REPO_TIMEOUT`       | `30`                                         | timeout setting for the repository         |
| `VELA_REPO_TRUSTED`       | `false`                                      | trusted setting for the repository         |
| `VELA_REPO_VISIBILITY`    | `public`                                     | visibility setting for the repository      |


#### User Environment Variables

| Key                    | Value                       | Explanation                        |
| ---------------------- | --------------------------- | ---------------------------------- |
| `VELA_USER_ACTIVE`     | `true`                      | active setting for the user        |
| `VELA_USER_ADMIN`      | `true`                      | admin platform status for the user |
| `VELA_USER_FAVORITES`  | `[ "octocat/hello-world" ]` | favorites starred for the user     |
| `VELA_USER_NAME`       | `Octocat`                   | user handle setting for the user   |