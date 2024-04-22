---
title: "Stages"
linkTitle: "Stages"
weight: 10
description: >
  Learn about stages pipelines.
---

A stages pipelines are designed to parallelize one-to-many sets of step tasks.

By design all of the stages will run at the same time unless the user uses a `needs:` YAML tag to control the flow of stage executions (see example).

Stages will also stop executing their steps if the build fails as a whole, by default. In other words, if stage 1 fails, the steps that have yet to execute in stage 2 will be skipped. The user can declare `independent: true` for any stage to change this behavior.

These pipelines do not have a minimum defined length and will always execute steps within a stage in the order defined. Stages always run on the same host so it's important to take into consideration the size of the worker running your builds.

In this pipeline both stages trigger at the same time.

Both steps are pulling a [Alpine Linux](https://alpinelinux.org/) image from [Docker Hub](https://hub.docker.com/) and executing echo statements.  

**See it in action with examples!**

* [Go](/docs/usage/examples/go_modules/)
* [Rust](/docs/usage/examples/rust_cargo/)
* [Gradle](/docs/usage/examples/java_gradle/)
* [Maven](/docs/usage/examples/java_maven/)
* [Node](/docs/usage/examples/node/)

You can learn more about stage orchestration [here](/docs/usage/stage_orchestration)!

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

{{% alert title="Note:" color="info" %}}
Be aware that `needs:` references stages by their name, which can be overridden by the `name` tag in the stage definition.
{{% /alert %}}

```sh
$ vela exec pipeline
...
[stage: greeting][step: Greeting] $ echo "Hello, World"
[stage: greeting][step: Greeting] Hello, World
[stage: welcome][step: Welcome] $ echo "Welcome to the Vela docs"
[stage: welcome][step: Welcome] Welcome to the Vela docs
[stage: goodbye][step: Goodbye] $ echo "Goodbye, World"
[stage: goodbye][step: Goodbye] Goodbye, World
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag),
