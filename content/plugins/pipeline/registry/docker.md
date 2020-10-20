---
title: "Docker"
---

## Overview

{{% alert color="warning" %}}
This plugin was originally used to build **all** Docker images. The functionality of this plugin still exists within [Kaniko](/docs/plugins/pipeline/registry/kaniko)
{{% /alert %}}

This plugin enables the ability to build and publish [Docker](https://www.docker.com/) images in a Vela pipeline. Plugin requires the pipeline to run on a worker that provides the plugin elevated access. 

Source Code: https://github.com/go-vela/vela-docker

Registry: https://hub.docker.com/r/target/vela-docker

## Usage

{{% alert color="warning" %}}
Users should refrain from using `latest` as the tag for the Docker image.

It is recommended to use a semantically versioned tag instead.
{{% /alert %}}

Sample of building and publishing an image:

```yaml
steps:
  - name: publish_hello-world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world:latest ]
```

Sample of building an image without publishing:

```diff
steps:
  - name: publish hello world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world:latest ]    
+     dry_run: true
```

Sample of building and publishing an image with custom tags:

```diff
steps:
  - name: publish hello world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
+     tags: 
+       - index.docker.io/octocat/hello-world:latest
+       - index.docker.io/octocat/hello-world:1
+       - index.docker.io/octocat/hello-world:foobar
```

Sample of building and publishing an image with build arguments:

```diff
steps:
  - name: publish hello world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world ]    
+     build_args:
+       - FOO=bar
```

Sample of building and publishing an image with image caching:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world:latest ]    
+     cache_from: index.docker.io/octocat/hello-world
```

Sample of building and publishing with custom daemon settings:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world:latest ]    
+     daemon: 
+       registry_mirror: mirror.index.docker.io
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

Users can use [Vela internal secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-docker:latest
    pull: always
+   secrets: [ docker_username, docker_password ]
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world:latest ] 
-     username: octocat
-     password: superSecretPassword
```

{{% alert color="info" %}}
This example will add the `secrets` to the `publish_hello-world` step as environment variables:

- `DOCKER_USERNAME=<value>`
- `DOCKER_PASSWORD=<value>`
{{% /alert %}}

### External

The plugin accepts the following files for authentication:

| Parameter  | Volume Configuration                                                                                                   |
| ---------- | ---------------------------------------------------------------------------------------------------------------------- |
| `password` | `/vela/parameters/docker/registry/password`, `/vela/secrets/docker/registry/password`, `/vela/secrets/docker/password` |
| `username` | `/vela/parameters/docker/registry/username`, `/vela/secrets/docker/registry/username`, `/vela/secrets/docker/username` |

Users can use [Vela external secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: publish_hello-world
    image: target/vela-docker:latest
    pull: always
    parameters:
      registry: index.docker.io
      tags: [ index.docker.io/octocat/hello-world:latest ] 
-     username: octocat
-     password: superSecretPassword
```

{{% alert color="info" %}}
This example will read the secrets values in the volume stored at `/vela/secrets/`:
{{% /alert %}}

## Parameters

{{% alert color="info" %}}
* the plugin supports reading all parameters via environment variables or files
* values set from a file take precedence over values set from the environment
* by default [build kit](https://docs.docker.com/develop/develop-images/build_enhancements/) is on, it can be turned off by setting `DOCKER_BUILDKIT=0` in the environment
* `key.key` syntax signifies a new yaml object within the definition. 
{{% /alert %}}

### Registry

The following parameters are used to configure the image:

| Name       | Description                                   | Required | Default           |
| ---------- | --------------------------------------------- | -------- | ----------------- |
| `dry_run`  | enables building the image without publishing | `false`  | `false`           |
| `registry` | Docker registry address to communicate with   | `true`   | `index.docker.io` |
| `password` | password for communication with the registry  | `true`   | N/A               |
| `username` | user name for communication with the registry | `true`   | N/A               |


### Build and Push

The following parameters are used to configure the image:

| Name                    | Description                                                                                                         | Required | Default |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | ------- |
| `add_hosts`             | enables adding a custom host-to-IP mapping - format (host:ip)                                                       | `false`  | N/A     |
| `build_args`            | enables setting build-time variables                                                                                | `false`  | N/A     |
| `cache_from`            | enables setting images to consider as cache sources                                                                 | `false`  | N/A     |
| `cgroup_parent`         | enables setting an optional parent cgroup for the container                                                         | `false`  | N/A     |
| `compress`              | enables setting compression the build context using gzip                                                            | `false`  | N/A     |
| `context`               | enables setting the build context                                                                                   | `true`   | `.`     |
| `cpu.period`            | enables setting limits on the CPU CFS (Completely Fair Scheduler) period                                            | `false`  | N/A     |
| `cpu.quota`             | enables setting limit on the CPU CFS (Completely Fair Scheduler) quota                                              | `false`  | N/A     |
| `cpu.shares`            | enables setting CPU shares (relative weight)                                                                        | `false`  | N/A     |
| `cpu.set_cpus`          | enables setting CPUs in which to allow execution (0-3, 0,1)                                                         | `false`  | N/A     |
| `cpu.set_mems`          | enables setting MEMs in which to allow execution (0-3, 0,1)                                                         | `false`  | N/A     |
| `disable_content_trust` | enables skipping image verification                                                                                 | `false`  | N/A     |
| `file`                  | enables setting the name of the Dockerfile                                                                          | `false`  | N/A     |
| `force_rm`              | enables setting always remove on intermediate containers                                                            | `false`  | N/A     |
| `image_id_file`         | enables setting writing the image ID to the file                                                                    | `false`  | N/A     |
| `isolation`             | enables container isolation technology                                                                              | `false`  | N/A     |
| `labels`                | enables setting metadata for an image                                                                               | `false`  | N/A     |
| `memory`                | enables setting a memory limit                                                                                      | `false`  | N/A     |
| `memory_swaps`          | enables setting a swap limit equal to memory plus swap: '-1' to enable unlimited swap                               | `false`  | N/A     |
| `network`               | enables setting the networking mode for the RUN instructions during build                                           | `false`  | N/A     |
| `no_cache`              | enables setting not use cache when building the image                                                               | `false`  | N/A     |
| `outputs`               | enables setting an output destination - format (type=local,dest=path)                                               | `false`  | N/A     |
| `platform`              | enables setting a platform if server is multi-platform capable                                                      | `false`  | N/A     |
| `progress`              | enables setting type of progress output - options (auto|plain|tty)                                                  | `false`  | N/A     |
| `pull`                  | enables always attempting to pull a newer version of the image                                                      | `false`  | N/A     |
| `quiet`                 | enables suppressing the build output and print image ID on success                                                  | `false`  | N/A     |
| `remove`                | enables removing the intermediate containers after a successful build                                               | `false`  | N/A     |
| `secrets`               | enables setting a secret file to expose to the build - format (id=mysecret,src=/local/secret)                       | `false`  | N/A     |
| `security_opts`         | enables setting security options                                                                                    | `false`  | N/A     |
| `shm_sizes`             | enables setting the size of /dev/shm                                                                                | `false`  | N/A     |
| `squash`                | enables setting squash newly built layers into a single new layer                                                   | `false`  | N/A     |
| `ssh_components`        | enables setting an ssh agent socket or keys to expose to the build - format (default|<id>[=<socket>|<key>[,<key>]]) | `false`  | N/A     |
| `stream`                | enables streaming attaches to server to negotiate build context                                                     | `false`  | N/A     |
| `tags`                  | enables naming and optionally a tagging - format (name:tag)                                                         | `true`   | N/A     |
| `target`                | enables setting the target build stage to build.                                                                    | `false`  | N/A     |
| `ulimits`               | enables setting ulimit options                                                                                      | `false`  | N/A     |

### Daemon

The following parameters are used to configure the image:

| Name                  | Description                                             | Required | Default |
| --------------------- | ------------------------------------------------------- | -------- | ------- |
| `bip`                 | enables specifying a network bridge IP                  | `false`  | N/A     |
| `dns.servers`         | enables setting the DNS server to use                   | `false`  | N/A     |
| `dns.searches`        | enables setting the DNS search domains to use           | `false`  | N/A     |
| `experimental`        | enable experimental features                            | `false`  | N/A     |
| `insecure_registries` | enables insecure registry communication                 | `false`  | N/A     |
| `ipv6`                | enables IPv6 networking                                 | `false`  | N/A     |
| `mtu`                 | enable setting the containers network MTU               | `false`  | N/A     |
| `registry_mirrors`    | enables setting a preferred Docker registry mirror      | `false`  | N/A     |
| `storage.drivers`     | enables setting an alternate storage driver             | `false`  | N/A     |
| `storage.opts`        | enables setting options on the alternate storage driver | `false`  | N/A     |


## Template

COMING SOON!

## Troubleshooting

Below are a list of common problems and how to solve them: