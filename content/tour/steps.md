---
title: "Steps"
linkTitle: "Steps"
weight: 8
description: >
  Learn about steps pipelines.
---

A steps pipeline is designed to run a sequential set of tasks.

These pipelines do not have a minimum defined length and steps will always execute in the order defined. 

In this pipeline each step is shown with the minimum required YAML tags to execute a step. 

Both steps are pulling a [Alpine Linux](https://alpinelinux.org/) image from [Docker Hub](https://hub.docker.com/) and executing echo statements.  

**See it in action with examples!**

* [Go](/docs/usage/examples/go_modules/)
* [Rust](/docs/usage/examples/rust_cargo/)
* [Gradle](/docs/usage/examples/java_gradle/)
* [Maven](/docs/usage/examples/java_maven/)
* [Node](/docs/usage/examples/node/)


<!-- section break -->

```yaml
version: "1"

# In this pipeline, commands are executed inside the container as the Entrypoint.
# If any command returns a non-zero exit code, the pipeline fails and exits.
steps:

  - name: Greeting
    image: alpine
    commands:
      - echo "Hello, World"

  - name: Welcome
    image: alpine
    commands:
      - echo "Welcome to the Vela docs"
```

```sh
$ vela exec pipeline
...
[stage: ][step: Greeting] $ echo "Hello, World"
[stage: ][step: Greeting] Hello, World
[stage: ][step: Welcome] $ echo "Welcome to the Vela docs"
[stage: ][step: Welcome] Welcome to the Vela docs  
```
<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag),
