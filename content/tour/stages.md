---
title: "Stages"
linkTitle: "Stages"
weight: 10
description: >
  Learn about stages pipelines.
---

A stages pipelines are designed to parallelize one-to-many sets of step tasks.

By design all of the stages will run at the same time unless the user uses a `needs:` YAML tag to control the flow of stage executions (see example). Note: even if every step within a stage is skipped, the stage still runs. Do not use `needs` as a stage-level equivalent to `rulesets`. 

These pipelines do not have a minimum defined length and will always execute steps within a stage in the order defined. Stages always run on the same host so it's important to take into consideration the size of the worker running your builds.

In this pipeline both stages trigger at the same time and run independently of the other. 

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
stages:
  greeting:
    steps:
      - name: Greeting
        image: alpine
        commands:
          - echo "Hello, World"

  welcome:
    steps:
      - name: Welcome
        image: alpine
        commands:
          - echo "Welcome to the Vela docs"
  
  goodbye:
    # will wait for greeting and welcome to finish
    needs: [greeting, welcome]
    steps:
      - name: Goodbye
        image: alpine
        commands:
          - echo "Goodbye, World"
```


```sh
$ vela exec pipeline
...
[stage: greeting][step: Greeting] $ echo "Hello, World"
[stage: greeting][step: Greeting] Hello, World
[stage: welcome][step: Welcome] $ echo "Welcome to the Vela docs"
[stage: welcome][step: Welcome] Welcome to the Vela docs
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag),
