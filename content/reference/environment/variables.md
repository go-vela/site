---
title: "Variables"
linkTitle: "Variables"
description: >
  Learn what environment variables are injected into containers
---

## Container Defaults

The following environment variables are injected into every step, service, or secret container.

#### Build Environment Variables

| Key                       | Value                                                       | Explanation                                                         |
| ------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------- |
| `VELA_BUILD_AUTHOR`       | `octocat`                                                   | author from the source commit                                       |
| `VELA_BUILD_AUTHOR_EMAIL` | `octocat@github.com`                                        | author email from the source commit, available only in `push` events                                 |
| `VELA_BUILD_BASE_REF`     | `refs/heads/dev`                                            | reference from the base commit                                      |
| `VELA_BUILD_BRANCH`       | `main`                                                      | branch from the source commit                                       |
| `VELA_BUILD_CHANNEL`      | `vela`                                                      | queue channel the build was published to                            |
| `VELA_BUILD_CLONE`        | `https://github.com/octocat/hello-world.git`                | clone url for the repository the build was triggered from           |
| `VELA_BUILD_COMMIT`       | `7fd1a60b01f91b314f59955a4e4d4e80d8edf11d`                  | commit sha from the source commit                                   |
| `VELA_BUILD_CREATED`      | `1556720958`                                                | unix timestamp representing build creation time                     |
| `VELA_BUILD_DISTRIBUTION` | `linux`                                                     | distribution where the build was executed                           |
| `VELA_BUILD_ENQUEUED`     | `1556720958`                                                | unix timestamp representing build enqueued time                     |
| `VELA_BUILD_EVENT`        | `push`                                                      | webhook event that triggered the build                              |
| `VELA_BUILD_HOST`         | `vela-worker-1`                                             | fully qualified domain name of the worker the build was executed on |
| `VELA_BUILD_LINK`         | `https://vela.example.com/octocat/hello-world/1`       | link to the build in the UI                                         |
| `VELA_BUILD_MESSAGE`      | `Merge pull request #6 from octocat/patch-1`                | message from the source commit                                      |
| `VELA_BUILD_NUMBER`       | `1`                                                         | build number                                                        |
| `VELA_BUILD_PARENT`       | `1`                                                         | previous build number                                               |
| `VELA_BUILD_REF`          | `refs/heads/main`                                           | reference from the source commit                                    |
| `VELA_BUILD_RUNTIME`      | `docker`                                                    | runtime where the build was executed                                |
| `VELA_BUILD_SENDER`       | `NealColeman`                                               | user who triggered the build                                        |
| `VELA_BUILD_STARTED`      | `1556730001`                                                | unix timestamp representing build start time                        |
| `VELA_BUILD_SOURCE`       | `https://github.com/octocat/hello-world/commit/7fd1a60b01f91b314f59955a4e4d4e80d8edf11d` |  full url for the source commit the build was triggered from                            |
| `VELA_BUILD_STATUS`       | `success`                                                   | status of the build                                                 |
| `VELA_BUILD_TITLE`        | `push received from https://github.com/octocat/hello-world` | title for the build                                                 |
| `VELA_BUILD_WORKSPACE`    | `/vela/src/github.com/octocat/hello-world`                  | working directory the build is executed in                          |

##### `comment` event only

{{% alert color="info" %}}
The following table includes variables only available during the **comment** event.
{{% /alert %}}

| Key                       | Value | Explanation                                                |
| ------------------------- | ----- | ---------------------------------------------------------- |
| `VELA_BUILD_PULL_REQUEST` | `1`   | pull request number is populated from the source reference |
| `VELA_PULL_REQUEST`       | `1`   | pull request number is populated from the source reference |

##### `deployment` event only

{{% alert color="info" %}}
The following table includes variables only available during the **deployment** event.

All custom parameters are passed to the deployment available with a `DEPLOYMENT_PARAMETER_` prefix of the key.
{{% /alert %}}

| Key                 | Value        | Explanation                                   |
| ------------------- | -----------  | --------------------------------------------- |
| `VELA_BUILD_TARGET` | `production` | name of target environment for the deployment |
| `VELA_DEPLOYMENT`   | `production` | name of target environment for the deployment |

##### `pull_request` event only

{{% alert color="info" %}}
The following table includes variables only available during the **pull_request** event.
{{% /alert %}}

| Key                        | Value  | Explanation                                                |
| -------------------------- | ------ | ---------------------------------------------------------- |
| `VELA_BUILD_PULL_REQUEST`  | `1`    | pull request number is populated from the source reference |
| `VELA_PULL_REQUEST`        | `1`    | pull request number is populated from the source reference |
| `VELA_PULL_REQUEST_SOURCE` | `dev`  | pull request branch from the source reference              |
| `VELA_PULL_REQUEST_TARGET` | `main` | pull request branch for the target reference               |

##### `tag` event only

{{% alert color="info" %}}
The following table includes variables only available during the **tag** event.
{{% /alert %}}

| Key              | Value    | Explanation                                |
| ---------------- | -------- | ------------------------------------------ |
| `VELA_BUILD_TAG` | `v1.0.0` | tag is populated from the source reference |


#### Vela Environment Variables

| Key              | Value                                             | Explanation                                                         |
| ---------------- |---------------------------------------------------|---------------------------------------------------------------------|
| `VELA`           | `true`                                            | environment is Vela                                                 |
| `VELA_ADDR`      | `vela.example.com`                           | fully qualified domain name of the Vela server                      |
| `VELA_CHANNEL`   | `vela`                                            | queue channel the build was published to                            |
| `VELA_DATABASE`  | `postgres`                                        | database Vela is connected to                                       |
| `VELA_HOST`      | `vela-worker-1`                                   | fully qualified domain name of the worker the build was executed on |
| `VELA_QUEUE`     | `redis`                                           | queue build was published to                                        |
| `VELA_RUNTIME`   | `docker`                                          | runtime environment build was executed in                           |
| `VELA_SOURCE`    | `github`                                          | queue channel the build was published to                            |
| `VELA_VERSION`   | `v0.1.0`                                          | Vela version                                                        |
| `VELA_WORKSPACE` | `/vela/src/github.com/github/octocat/hello-world` | working directory the build is executed in                          |
| `CI`             | `true`                                            | Indicates this is a CI environment                                  |

#### Repository Environment Variables

| Key                       | Value                                        | Explanation                                   |
| ------------------------- | -------------------------------------------- | --------------------------------------------- |
| `VELA_REPO_ACTIVE`        | `true`                                       | active setting for the repository             |
| `VELA_REPO_ALLOW_COMMENT` | `false`                                      | comment enabled setting for the repository    |
| `VELA_REPO_ALLOW_DEPLOY`  | `false`                                      | deploy enabled setting for the repository     |
| `VELA_REPO_ALLOW_PULL`    | `true`                                       | pull enabled setting for the repository       |
| `VELA_REPO_ALLOW_PUSH`    | `true`                                       | push enabled setting for the repository       |
| `VELA_REPO_ALLOW_TAG`     | `false`                                      | tag enabled setting for the repository        |
| `VELA_REPO_BRANCH`        | `main`                                       | default branch of the repository              |
| `VELA_REPO_BUILD_LIMIT`   | `10`                                         | limit of concurrent builds for the repository |
| `VELA_REPO_CLONE`         | `https://github.com/octocat/hello-world.git` | clone url of the repository                   |
| `VELA_REPO_FULL_NAME`     | `octocat/hello-world`                        | full name of the repository                   |
| `VELA_REPO_LINK`          | `https://github.com/octocat/hello-world`     | direct url of the repository                  |
| `VELA_REPO_NAME`          | `hello-world`                                | name of the repository                        |
| `VELA_REPO_ORG`           | `octocat`                                    | org of the repository                         |
| `VELA_REPO_PRIVATE`       | `false`                                      | privacy setting for the repository            |
| `VELA_REPO_TIMEOUT`       | `30`                                         | timeout setting for the repository            |
| `VELA_REPO_TRUSTED`       | `false`                                      | trusted setting for the repository            |
| `VELA_REPO_VISIBILITY`    | `public`                                     | visibility setting for the repository         |

#### User Environment Variables

| Key                    | Value                       | Explanation                        |
| ---------------------- | --------------------------- | ---------------------------------- |
| `VELA_USER_ACTIVE`     | `true`                      | active setting for the user        |
| `VELA_USER_ADMIN`      | `true`                      | admin platform status for the user |
| `VELA_USER_FAVORITES`  | `[ "octocat/hello-world" ]` | favorites starred for the user     |
| `VELA_USER_NAME`       | `Octocat`                   | user handle setting for the user   |

## Step Only Defaults

The following environment variables are **only** injected into every step container.

| Key                      | Value                    | Explanation                                                        |
| ------------------------ | ------------------------ | ------------------------------------------------------------------ |
| `VELA_STEP_CREATED`      | `1556720958`             | unix timestamp representing step creation time                     |
| `VELA_STEP_DISTRIBUTION` | `linux`                  | distribution where the step was executed                           |
| `VELA_STEP_EXIT_CODE`    | `0`                      | exit code of the step when container starts                        |
| `VELA_STEP_HOST`         | `vela-worker-1`          | fully qualified domain name of the worker the step was executed on |
| `VELA_STEP_IMAGE`        | `target/vela-git:latest` | name of the image executed                                         |
| `VELA_STEP_NAME`         | `clone`                  | name of the step                                                   |
| `VELA_STEP_NUMBER`       | `1`                      | number of the step executed within the pipeline                    |
| `VELA_STEP_RUNTIME`      | `docker`                 | runtime where the step was executed                               |
| `VELA_STEP_STAGE`        | `clone`                  | name of the stage the step belongs to within the pipeline          |
| `VELA_STEP_STARTED`      | `1556730001`             | unix timestamp representing step start time                       |
| `VELA_STEP_STATUS`       | `success`                | status of the step                                                 |

## Service Only Defaults

The following environment variables are **only** injected into every step container.

| Key                         | Value                    | Explanation                                                           |
| --------------------------- | ------------------------ | --------------------------------------------------------------------- |
| `VELA_SERVICE_CREATED`      | `1556720958`             | unix timestamp representing service creation time                     |
| `VELA_SERVICE_DISTRIBUTION` | `linux`                  | distribution where the service was executed                           |
| `VELA_SERVICE_EXIT_CODE`    | `0`                      | exit code of the service when container starts                        |
| `VELA_SERVICE_HOST`         | `vela-worker-1`          | fully qualified domain name of the worker the service was executed on |
| `VELA_SERVICE_IMAGE`        | `target/vela-git:latest` | name of the image executed                                            |
| `VELA_SERVICE_NAME`         | `clone`                  | name of the service                                                   |
| `VELA_SERVICE_NUMBER`       | `1`                      | number of the service executed within the pipeline                    |
| `VELA_SERVICE_RUNTIME`      | `docker`                 | runtime where the service was executed                                  |
| `VELA_SERVICE_STARTED`      | `1556730001`             | unix timestamp representing service start time                          |
| `VELA_SERVICE_STATUS`       | `success`                | status of the service                                                 |
