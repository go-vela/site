---
title:  "Workspace"
toc:  true
weight:  6
description: >
  Shared directory that all build steps begin at.
---

### Cloning

Vela automatically checks out the repository into a local volume that is mounted into each Docker container. This volume is generally referred to as a workspace, which defines the working directory shared by all steps in a build.

```sh
git clone https://github.com/octocat/hello-world.git <workspace>
```

### Working Directory

This ensures the code, dependencies, and compiled binaries are persisted and shared between the steps. The default workspace attached to every build is unique and matches the below pattern:

```sh
# Syntax
/home/<source org>_<source repo>_<build number>

# Example
/home/octocat_hello-world_1
```

This would be the equivalent to the following Docker commands being executed:

```sh
docker volume create build-workspace

docker run --volume=build-workspace:/home/octocat_hello-world_1 <image>
```
