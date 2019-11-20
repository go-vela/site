---
title: "Write a Pipeline"
linkTitle: "Write a Pipeline"
weight: 4
description: >
  Learn how to write your first pipeline.
---

Get started by placing a .vela.yml file in the root of your repository. Below is an example .vela.yml with a single “Hello World” step.

```yaml
version: "1"

steps:
  - name: Hello_World
    image: alpine:latest
    commands:
      - echo "Hello World"
```

You can break your build into multiple named steps (see below example). Each step executes in a separate Docker container with shared disk access to your project workspace.

```yaml
steps:
  - name: Hello
    image: alpine:latest
    commands:
      - echo "Hello"

  - name: World
    image: alpine:latest
    commands:
      - echo "World"
```

Note that the above step names are completely arbitrary. You can call them whatever you like.

### Images

Vela executes your build inside a Docker image with the workspace mounted. This means you don’t have to setup or install any repository dependencies on your host machine. Use any valid Docker image in any Docker registry as your build environment.

```yaml
steps:
  - name: build
    image: golang:1.6
```

### Cloning

Vela automatically clones your repository into a local volume, the workspace, that is mounted into each Docker container. The workspace is available to all steps in your build process, including plugins and service containers.

### Commands

Vela allows you to specify commands that are executed within the default shell inside your build container. By default commands use the root of your repository as the working directory.

```yaml
steps:
  - name build
    image: golang
    commands:
      - go get
      - go build
      - go test
```

### Ruleset

Rulesets allow you to specify when a step will be triggered. You can restrict a step to a specific condition or specify a rule to specify to run unless a condition is met. You can read more in the pipeline docs.

```yaml
steps:
  - name: Hello_World
    image: alpine:latest
    ruleset:
      branch: master
      event: push
    commands:
      - echo "Hello World"
```
