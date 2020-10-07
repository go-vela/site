---
title: "Makisu"
---

## Description

This plugin uses [Kaniko](https://github.com/uber/makisu) to provide the ability to build and publish [Docker](https://www.docker.com/) images in a Vela pipeline without elevated access on the workers.

Source Code: https://github.com/go-vela/vela-makisu

Registry: https://hub.docker.com/r/target/vela-makisu

## Usage

{{% alert color="tip" %}}
* It is not recommended to use `latest` as the tag for the Docker image. Users should use a semantically versioned tag instead.
{{% /alert %}}

Sample of building and publishing an image:

```yaml
steps:
  - name: publish_hello-world
    image: target/vela-makisu:latest
    pull: always
    parameters:
      registry: index.docker.io
      tag: index.docker.io/octocat/hello-world
      pushes: [ index.docker.io ]
```

Sample of building an image without publishing:

```diff
steps:
  - name: publish hello world
    image: target/vela-makisu:latest
    pull: always
    parameters:
-     pushes: [ index.docker.io ]
      registry: index.docker.io
      tag: index.docker.io/octocat/hello-world:latest
```

Sample of building and publishing an image with custom tags:

```diff
steps:
  - name: publish hello world
    image: target/vela-makisu:latest
    pull: always
    parameters:
      registry: index.docker.io
      tag: index.docker.io/octocat/hello-world:latest
      pushes: [ index.docker.io ]
+     replicas:
+       - index.docker.io/octocat/hello-world:1
+       - index.docker.io/octocat/hello-world:foobar
```

Sample of building and publishing an image with build arguments:

```diff
steps:
  - name: publish hello world
    image: target/vela-makisu:latest
    pull: always
    parameters:
+     build_args:
+       - FOO=bar
      registry: index.docker.io
      tag: index.docker.io/octocat/hello-world
      pushes: [ index.docker.io ]
```

Sample of building and publishing an image with redis caching:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-makisu:latest
    pull: always
    parameters:
+     redis_cache_options: 
+       addr: redis.company.com
+       password: superSecretPassword
+       ttl: 7d
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
      pushes: [ index.docker.io ]
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
    image: target/vela-makisu:latest
    pull: always
+   secrets: [ docker_username, docker_password, redis_cache ]
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
      pushes: [ index.docker.io ]
-     redis_cache: 
-       addr: redis.company.com
-       password: superSecretPassword
-       ttl: 7d      
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
| `password`  | `/vela/parameters/makisu/registry/password`, `/vela/secrets/makisu/registry/password`, `/vela/secrets/makisu/password` |
| `username`  | `/vela/parameters/makisu/registry/username`, `/vela/secrets/makisu/registry/username`, `/vela/secrets/makisu/username` |

Users can use [Vela external secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-makisu:latest
    pull: always
    parameters:
      registry: index.docker.io
      repo: index.docker.io/octocat/hello-world
      pushes: [ index.docker.io ]
-     redis_cache: 
-       addr: redis.company.com
-       password: superSecretPassword
-       ttl: 7d      
-     username: octocat
-     password: superSecretPassword
```

## Parameters

{{% alert color="info" %}}
* the plugin supports reading all parameters via environment variables or files
* values set from a file take precedence over values set from the environment
{{% /alert %}}

The following parameters are used to configure the build and push process:

| Name              | Description                                                          | Required | Default |
| ----------------- | -------------------------------------------------------------------- | -------- | ------- |
| `build_args`      | build time arguments for the Dockerfile                              | `false`  | `N/A`   |
| `commit`          | commit info for #!COMMIT annotations                                 | `false`  | `N/A`   |
| `compression`     | compression on the tar file built - options: (no|speed|size|default) | `false`  | `N/A`   |
| `context`         | the context for the image to be built                                | `false`  | `.`     |
| `deny_list`       | list of locations to be ignored within docker image                  | `false`  | `N/A`   |
| `docker`          | configuration on the docker daemon                                   | `false`  | `N/A`   |
| `destination`     | the output of the tar file                                           | `false`  | `N/A`   |
| `file`            | a the absolute path to dockerfile                                    | `false`  | `info`  |
| `http_cache`      | custom http options caching                                          | `false`  | `N/A`   |
| `load`            | enables loading a docker image into the docker daemon post build     | `false`  | `N/A`   |
| `local_cache_ttl` | a time to live for the local docker cache (default 168h0m0s)         | `false`  | `N/A`   |
| `modify_fs`       | makisu to modify files outside its internal storage directories      | `false`  | `N/A`   |
| `perserve_root`   | copying storage from root in the storage during and after build      | `false`  | `N/A`   |
| `pushes`          | registries to push the image to                                      | `false`  | `N/A`   |
| `redis_cache`     | custom redis server for caching                                      | `false`  | `N/A`   |
| `replicas`        | pushing image to alternative targets i.e. `<registry>/<repo>:<tag>`  | `false`  | `N/A`   |
| `storage`         | a directory for makisu to use for temp files and cached layers       | `false`  | `N/A`   |
| `tag`             | the tag for an image                                                 | `true`   | `N/A`   |
| `storage`         | the target build stage to build                                      | `false`  | `N/A`   |

The following parameters are used to configure the registry:

| Name            | Description                                                        | Required | Default           |
| --------------- | ------------------------------------------------------------------ | -------- | ----------------- |
| `mirror`        | name of the mirror registry to use                                 | `false`  | `N/A`             |
| `password`      | password for communication with the registry                       | `true`   | `N/A`             |
| `registry`      | name of the registry for the repository                            | `true`   | `index.docker.io` |
| `repo`          | name of the repository for the image                               | `true`   | `N/A`             |
| `username`      | user name for communication with the registry                      | `true`   | `N/A`             |

## Template

COMING SOON!

## Troubleshooting

Below are a list of common problems and how to solve them:

COMING SOON!