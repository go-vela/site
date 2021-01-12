---
title: "Building Docker Images"
toc: true
description: >
  Understanding the options for how to build a Dockerfile
---

We assume you understand how to build and run Docker images. If you need assistance on how to get started with Docker; we recommend you see their documentation for [getting set up](https://docs.docker.com/get-started/).

Vela runs all workloads within Docker containers. Which essentially gives us two core different ways to build Docker images:

* Without elevated daemon access
* With elevated daemon access

Both options have disadvantages and advantages, so we encourage all Vela administrators to weigh the pros/cons of how they want to build Docker images for their cluster.

## Without elevated daemon access

Building an image without elevated access gives administrators the most secure pattern for not allowing any elevated access to the workers within the cluster. There are two plugin options for building those images:

* [vela-kaniko](/docs/plugins/pipeline/registry/kaniko/)
* [vela-makisu](/docs/plugins/pipeline/registry/makisu/)

We recommend customers read the [tool comparisons](/docs/usage/getting-started/docker/#additional-resources) before picking a technology for building their images. In-depth examples for building with either utility are available within their respective plugin documentation pages. A simple example is provided below:

```diff
version: "1"
steps:
+ - name: build and publish with kaniko
+   image: target/vela-kaniko:latest
+   pull: always
+   parameters:
+     registry: index.docker.io
+     repo: index.docker.io/octocat/hello-world

+ - name: build and publish with makisu
+   image: target/vela-makisu:latest
+   pull: always
+   parameters:
+     registry: index.docker.io
+     tag: index.docker.io/octocat/hello-world
+     pushes: [ index.docker.io ]
```

## With elevated daemon access

Building an image with elevated access is a allowed pattern as long as the administrators have set the required allow list of images on the worker. It's *important to work with your administrator* to understand stand which pattern you instances was deployed to support. The supported plugin for building those images:

* [vela-kaniko](/docs/plugins/pipeline/registry/docker/)

```diff
version: "1"
steps:
+ - name: build and publish with Dockers build kit
+   image: target/vela-docker:latest
+   pull: always
+   parameters:
+     registry: index.docker.io
+     tags: [ index.docker.io/octocat/hello-world ]

+ - name: build and publish with Dockers without build kit
+   image: target/vela-docker:latest
+   environment:
+     DOCKER_BUILDKIT=0   
+   pull: always
+   parameters:
+     registry: index.docker.io
+     tags: [ index.docker.io/octocat/hello-world ]
```

## Additional Resources

* [Building Container Images Securely on Kubernetes](https://blog.jessfraz.com/post/building-container-images-securely-on-kubernetes/)
* [Why is building rootless so hard?](https://github.com/opencontainers/runc/pull/1692)
* [Introducing Makisu](https://eng.uber.com/makisu/)
* [Kaniko tools comparison](https://github.com/GoogleContainerTools/kaniko#comparison-with-other-tools)
* [Makisu tools comparison](https://github.com/uber/makisu#comparison-with-similar-tools)