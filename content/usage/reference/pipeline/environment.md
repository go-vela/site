---
title: "Environment"
linkTitle: "Environment"
weight: 5
description: >
  Reference for variables that are injected into a pipeline.
---

## Defaults

All environment variables specified in the tables below are injected into every step.

#### Build Environment Variables

| Key               | Value                                                                                    | Explanation                                                         |
| ----------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `BUILD_BRANCH`    | `master`                                                                                 | branch from the source commit                                       |
| `BUILD_CHANNEL`   | `vela`                                                                                   | queue channel the build was published to                            |
| `BUILD_COMMIT`    | `7fd1a60b01f91b314f59955a4e4d4e80d8edf11d`                                               | commit sha from the source commit                                   |
| `BUILD_CREATED`   | `1556720958`                                                                             | unix timestamp representing build creation time                     |
| `BUILD_ENQUEUED`  | `1556730001`                                                                             | unix timestamp representing build enqueue time                      |
| `BUILD_EVENT`     | `push`                                                                                   | webhook event that triggered the build                              |
| `BUILD_FINISHED`  | `1556730045`                                                                             | unix timestamp representing build completion time                   |
| `BUILD_HOST`      | `vela-worker-1`                                                                          | fully qualified domain name of the worker the build was executed on |
| `BUILD_MESSAGE`   | `New line at end of file.`                                                               | message from the source commit                                      |
| `BUILD_NUMBER`    | `1`                                                                                      | build number                                                        |
| `BUILD_PARENT`    | `1`                                                                                      | previous build number                                               |
| `BUILD_REF`       | `refs/heads/master`                                                                      | reference from the source commit                                    |
| `BUILD_STARTED`   | `1556730001`                                                                             | unix timestamp representing build start time                        |
| `BUILD_SOURCE`    | `https://github.com/octocat/hello-world/commit/7fd1a60b01f91b314f59955a4e4d4e80d8edf11d` | link from the source commit                                         |
| `BUILD_TITLE`     | `Merge pull request #6 from octocat/patch-1`                                             | title from the source commit                                        |
| `BUILD_WORKSPACE` | `/home/octocat_hello-world_1`                                                            | working directory the build is executed in                          |
| `BUILD_TAG`       | `v1.0.0`                                                                                 | tag is populated from the source reference                          |

_`BUILD_TAG` is only populated during tag events._

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
| `VELA_SOURCE`    | `https://github.com`          | queue channel the build was published to                            |
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
