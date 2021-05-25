---
title: "Understanding the Workspace"
toc: true
description: >
  Shared directory that all build steps begin at.
---

Vela uses a shared volume model between steps to allow shared file system during the build process. These volumes should be considered ephemeral in the sense once a build completes execution all data via the volume being destroyed.

## Working Directory

This ensures the configuration, code, dependencies, and compiled binaries are persisted and shared between the steps. The default workspace attached to every build is unique and matches the below pattern:

**Source:**

```sh
# Syntax
/vela/src/<source_provider/<source org>/<source repo>

# Example
/vela/src/github.com/go-vela/hello-world
```

**Secrets:**

```sh
# Syntax
/vela/secrets/<path>/<key>

# Example
/vela/secrets/github/username/
/vela/secrets/github/password/
```

**Parameters:**

```sh
# Syntax
/vela/parameters/<path>/<key>

# Example
/vela/parameters/github/repo/settings/topics
```

{{% alert color="warning" %}}
Before you use the parameters volume check the plugin authors docs to ensure it has support to read from `/vela/parameters`
{{% /alert %}}

This would be the equivalent to the following Docker commands being executed:

```sh
docker volume create build-workspace

docker run --volume=build-workspace:/vela/ <image>
```

## Cloning

Vela automatically checks out the repository into a local volume that is mounted into each Docker container. This volume is generally referred to as a workspace, which defines the working directory shared by all steps in a build.

```sh
git clone https://github.com/go-vela/hello-world.git <workspace>
```
{{% alert color="warning" %}}
In cases where your clone needs special configuration you should add a step at the beginning of the pipeline adding the desired behavior.
{{% /alert %}}
