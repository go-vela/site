---
title: "Stages"
linkTitle: "Stages"
weight: 9
description: >
  Learn about stages pipelines.
---

A stages pipelines are designed to parallelize one-to-many sets of step tasks.

By design all of the stages will run at the same time unless the user uses a `needs:` YAML tag to control the flow of stage executions.

These pipelines do not have a minimum defined length and will always execute steps within a stage in the order defined. 

In this pipeline both stages trigger at the same time and run independently of the other. 

Both steps are pulling a [Alpine Linux](https://alpinelinux.org/) image from [Docker Hub](https://hub.docker.com/) and executing echo statements.  

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