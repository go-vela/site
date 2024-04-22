---
title: "Stage Orchestration"
linkTitle: "Stage Orchestration"
description: >
  Learn how to orchestrate pipelines with stages.
---

This page will focus on [`stages`](/docs/tour/stages) and how to effectively leverage the orchestration options given to users. These options are: the [`ruleset`](/docs/tour/rulesets) tag, the [`needs`](/docs/reference/yaml/stages/#the-needs-tag) tag, and the [`independent`](/docs/reference/yaml/stages/#the-independent-tag) tag.

### Step Rulesets in Stages
To begin, let's focus on the `ruleset` tag. While this is not a tag at the stages level, each stage has a collection of steps, which can all be given rulesets. There are two kinds of rules within Vela: compile-time rules (path, event, branch, comment, tag, target, and repo) and a runtime rule (status). When Vela compiles a pipeline, it will purge any steps that do not meet the compile-time rules.

For example, let's consider a pipeline written as such:

```yaml
version: "1"

stages:
  build:
    steps:
      - name: Build My Code 
        image: golang:latest
        environment:
          CGO_ENABLED: '0'
          GOOS: linux
        commands:
          - go build

  deploy:
    steps:
      - name: Publish My Docker Image
        image: target/vela-kaniko:latest
        ruleset:
          event: push
          branch: main
        parameters:
          registry: index.docker.io
          repo: index.docker.io/octocat/hello-world
          dry-run: false
  notify:
    needs: [ build, deploy ]
    steps:
      - name: Report Failure
        image: target/vela-slack:latest
        ruleset:
          status: failure
        parameters:
          text: "Failure!"       
```

If a Vela build is triggered on a `push` to a branch named `issue-123`, the pipeline will be compiled like this:

```yaml
version: "1"

stages:
  build:
    steps:
      - name: Build My Docker Image
        image: target/vela-kaniko:latest
        parameters:
          registry: index.docker.io
          repo: index.docker.io/octocat/hello-world
          dry-run: true
  notify:
    needs: [ build ]
    steps:
      - name: Report Failure
        image: target/vela-slack:latest
        ruleset:
          status: failure
        parameters:
          text: "Failure!" 
```

Notice how the `deploy` stage has been pruned completely, rather than being a stage with empty steps. Further, since the `notify` stage normally waits on both `build` and `deploy`, in this situation, it only waits on `build`. The `notify` stage is still part of the build since its ruleset consists of only a runtime rule.

### Understanding the `needs` tag

While there isn't a sure-fire way of running stages in order, the `needs` tag introduces a level of dependency that can be used to order stages. However the `needs` tag can become tricky when combined with pruning, as shown in the example above. Let's take a look at a theoretical pipeline:

```yaml
version: "1"

stages:
  run-first:
    steps:
      - name: sleep for 10
        image: alpine:latest
        commands:
          - sleep 10
          - echo "done""

  runtime-ruleset-stage:
    needs: [ run-first ]
    steps:
      - name: fail
        image: alpine:latest
        ruleset:
          status: failure
        commands:
          - echo "runtime rule"

  compile-time-ruleset-stage:
    needs: [ run-first ]
    steps:
      - name: pruned
        image: alpine:latest
        ruleset:
          branch: not-main
        commands:
          - echo "never ran"

  x-stage:
    needs: [ runtime-ruleset-stage, compile-time-ruleset-stage ]
    steps:
      - name: who ran the build
        image: alpine:latest
        commands:
          - sleep 20
          - echo $VELA_BUILD_AUTHOR

  y-stage:
    needs: [ compile-time-ruleset-stage ]
    steps:
      - name: what repo is this
        image: alpine:latest
        commands:
          - sleep 20
          - echo $VELA_REPO_FULL_NAME
```

{{% alert title="Note:" color="info" %}}
Be aware that `needs:` references stages by their name, which can be overridden by the `name` tag in the stage definition.
{{% /alert %}}

Consider a Vela build triggered by a `push` to `main`. We know that `run-first` will indeed run first, followed by `runtime-ruleset-stage` since it cannot be pruned due to its runtime rule. However, if we recall from our first example, when the _entirety_ of a stage's step collection is pruned at compile-time, the stage disappears completely:

```yaml
version: "1"

stages:
  run-first:
    steps:
      - name: sleep for 10
        image: alpine:latest
        commands:
          - sleep 10
          - echo "done""

  runtime-ruleset-stage:
    needs: [ run-first ]
    steps:
      - name: fail
        image: alpine:latest
        ruleset:
          status: failure
        commands:
          - echo "runtime rule"

  x-stage:
    needs: [ runtime-ruleset-stage ]
    steps:
      - name: who ran the build
        image: alpine:latest
        commands:
          - sleep 20
          - echo $VELA_BUILD_AUTHOR

  y-stage:
    needs: [ ]
    steps:
      - name: what repo is this
        image: alpine:latest
        commands:
          - sleep 20
          - echo $VELA_REPO_FULL_NAME
```

So in fact, in this scenario, the `run-first` stage and the `y-stage` begin simultaneously, even though `y-stage` "needed" `compile-time-ruleset-stage` which "needed" `run-first` in the original pipeline. 

### Leveraging Stage independence

With the increasing popularity of monorepos, some Vela pipelines may want to simultaneously execute very different build flows based on modules within the repository. Since by nature Vela stages will skip the remainder of the build if a single stage fails its pipeline, this could potentially cause issues, such as half-done deployments.

For example, say we have a repo that has back-end _and_ front-end code written together. Let's assume all the back-end code is in `org/repo/back-end` and the front-end code is in `org/repo/front-end`. We can leverage the [`path`](/docs/reference/yaml/steps/#the-ruleset-tag) ruleset with the [`independent`](/docs/reference/yaml/stages/#the-independent-tag) stage tag to compartmentalize Vela builds:

```yaml
version: "1"

stages:
  test-and-build-backend:
    independent: true
    steps:
      - name: install go
        image: golang:latest
        pull: always
        ruleset:
          matcher: regexp
          path: org/repo/back-end/*
        environment:
          CGO_ENABLED: '0'
          GOOS: linux
        commands:
          - go get ./...

      - name: test go
        image: golang:latest
        pull: always
        ruleset:
          matcher: regexp
          path: org/repo/back-end/*
        environment:
          CGO_ENABLED: '0'
          GOOS: linux
        commands:
          - go test ./...

      - name: build go
        image: golang:latest
        pull: always
        ruleset:
          matcher: regexp
          path: org/repo/back-end/*
        environment:
          CGO_ENABLED: '0'
          GOOS: linux
        commands:
          - go build

  test-and-build-frontend:
    independent: true
    steps:
      - name: install node
        image: node:latest
        pull: always
        ruleset:
          matcher: regexp
          path: org/repo/front-end/*
        commands:
          - node install

      - name: lint node
        image: node:latest
        pull: always
        ruleset:
          matcher: regexp
          path: org/repo/front-end/*
        commands:
          - node test

      - name: build node
        image: node:latest
        pull: always
        ruleset:
          matcher: regexp
          path: org/repo/front-end/*
        commands:
          - node build
```

We can extend this example to deployments, and it's easy to see where a team may want one module to complete its build flow even if there's a failure in another module. 

### In Summary

Stages are an advanced tool to help with writing powerful and sensible pipelines with parallel execution. While these orchestration tools are helpful, consider just using `steps` to simplify pipelines that don't need the, sometimes surprising, complexity.
