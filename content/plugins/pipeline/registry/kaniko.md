---
title: "Kaniko"
---

## Overview

This plugin uses [Kaniko](https://github.com/GoogleContainerTools/kaniko) to provide the ability to build and publish [Docker](https://www.docker.com/) images in a Vela pipeline without evaluated access on the workers.

Source Code: https://github.com/go-vela/vela-kaniko

Registry: https://hub.docker.com/r/target/vela-kaniko

## Usage

{{% alert color="tip" %}}
* It is not recommended to use `latest` as the tag for the Docker image. Users should use a semantically versioned tag instead.
{{% /alert %}}

Sample of building and publishing an image:

```yaml
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

Sample of building an image without publishing:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
+     dry_run: true
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

Sample of building and publishing an image with custom tags:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
+     tags:
+       - latest
+       - foobar
```

Sample of building and publishing an image with automatic tags:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
+     auto_tag: true
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

Sample of building and publishing an image with build arguments:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
+     build_args:
+       - FOO=bar
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

Sample of building and publishing an image with caching:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
+     cache: true
+     cache_repo: index.docker.io/octocat/hello-world
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

Sample of building and publishing an image with custom labels:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
+     labels:
+       - FOO=bar
+       - HELLO=world
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.
{{% /alert %}}

### Internal

The plugin accepts the following `parameters` for authentication:

| Parameter   | Environment Variable Configuration                           |
| ----------- | ------------------------------------------------------------ |
| `password`  | `DOCKER_PASSWORD`, `REGISTRY_PASSWORD`, `PARAMETER_PASSWORD` |
| `username`  | `DOCKER_USERNAME`, `REGISTRY_USERNAME`, `PARAMETER_USERNAME` |

Users can use [Vela secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
+   secrets: [ docker_username, docker_password ]
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
-     username: octocat
-     password: superSecretPassword
```

{{% alert color="info" %}}
This example will add the `secrets` to the `publish_hello-world` step as environment variables:

- `DOCKER_USERNAME`=<value>
- `DOCKER_PASSWORD`=<value>
{{% /alert %}}

### External

The plugin accepts the following files for authentication:

| Parameter   | Volume Configuration                           |
| ----------- | ------------------------------------------------------------ |
| `password`  | `/vela/parameters/docker/registry/password`, `/vela/secrets/docker/registry/password`, `/vela/secrets/docker/password` |
| `username`  | `/vela/parameters/docker/registry/username`, `/vela/secrets/docker/registry/username`, `/vela/secrets/docker/username` |

Users can use [Vela external secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
-     username: octocat
-     password: superSecretPassword
```

{{% alert color="info" %}}
This example will read the secrets values in the volume stored at `/vela/secrets/`:
{{% /alert %}}

## Parameters

{{% alert color="info" %}}
* Vela injects several variables, by default, that this plugin can load in automatically.
* the plugin supports reading all parameters via environment variables or files
* values set from a file take precedence over values set from the environment
{{% /alert %}}

The following parameters are used to configure the image:

| Name         | Description                                   | Required | Default           |
| ------------ | --------------------------------------------- | -------- | ----------------- |
| `auto_tag`   | enables tagging of image automatically        | `false`  | `false`           |
| `build_args` | variables passed to image at build-time       | `false`  | `N/A`             |
| `cache`      | enable caching of image layers                | `false`  | `false`           |
| `cache_repo` | specific repo to enable caching for           | `false`  | `N/A`             |
| `context`    | path to context for building the image        | `true`   | `.`               |
| `dockerfile` | path to the file for building the image       | `true`   | `Dockerfile`      |
| `dry_run`    | enable building the image without publishing  | `false`  | `false`           |
| `event`      | event generated for build                     | `true`   | **set by Vela**   |
| `labels`     | unique labels to add to the image             | `false`  | `N/A`             |
| `log_level`  | set the log level for the plugin              | `true`   | `info`            |
| `password`   | password for communication with the registry  | `true`   | `N/A`             |
| `registry`   | name of the registry for the repository       | `true`   | `index.docker.io` |
| `repo`       | name of the repository for the image          | `true`   | `N/A`             |
| `sha`        | SHA-1 hash generated for commit               | `true`   | **set by Vela**   |
| `tag`        | tag generated for build                       | `false`  | **set by Vela**   |
| `tags`       | unique tags of the image                      | `true`   | `latest`          |
| `target`     | set the target build stage                    | `false`  | `N/A`             |
| `username`   | user name for communication with the registry | `true`   | `N/A`             |

## Template

COMING SOON!

## Troubleshooting

You can start troubleshooting this plugin by tuning the level of logs being displayed:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-kaniko:latest
    pull: always
    parameters:
+     log_level: trace
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
```

Below are a list of common problems and how to solve them:

COMING SOON!
