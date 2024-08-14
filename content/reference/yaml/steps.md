---
title: "Steps"
linkTitle: "Steps"
weight: 6
description: >
  YAML keys for steps block
---

The steps key is intended to be used to run sequential tasks in a pipeline.

```yaml
---
# This document is displaying all the required keys
# to run a postgres database for the duration of a pipeline.
steps: 
  - name: Hello World
    image: alpine:latest
    commands:
      - echo "Hello, Vela User"
```

## Keys

| Key           | Required | Type            | Description                                                      |
|---------------|----------|-----------------|------------------------------------------------------------------|
| `name`        | Y        | string          | Unique identifier for the container in the pipeline.             |
| `image`       | Y        | string          | Docker image used to create ephemeral container.                 |
| `pull`        | N        | string          | Declaration to configure if and when the Docker image is pulled. |
| `secrets`     | N        | struct          | Sensitive variables injected into the container environment.     |
| `environment` | N        | map || []string | Variables to inject into the container environment.              |
| `ruleset`     | N        | struct          | Conditions to limit the execution of the container.              |
| `parameters`  | N        | map             | Extra configuration variables specific to a plugin.              |
| `commands`    | N        | []string        | Execution instructions to run inside the container.              |
| `template`    | N        | struct          | Name of a template to expand in the pipeline.                      |
| `entrypoint`  | N        | []string        | Commands to execute inside the container.                        |
| `detach`      | N        | []string        | Run the container in a detached (headless) state.                |                                |
| `ulimits`     | N        | string          | Set the user limits for the container.                           |                        |
| `user`        | N        | string          | Set the user for the container. |

### Usage

#### The `name:` key

```yaml
---
steps:
    # Unique identifier for the container in the pipeline.
  - name: Hello World
```

#### The `image:` key

```yaml
---
steps:
    # Docker image used to create ephemeral container. 
  - image: alpine:latest
```

#### The `pull:` key

```yaml
---
steps:
    # Declaration to configure if and when the Docker image is pulled.
    # By default, the compiler will inject pull with value not_present but
    # accepts the following values: always, never, not_present, on_start
  - pull: always
```

#### The `secrets:` key

```yaml
---
steps:
    # Sensitive variables to injected into the container
    # environment as upper case env. i.e. GIT_USERNAME=vela
  - secrets: [ git_username ]
```

```yaml
---
steps:
    # Sensitive variables to injected into the container
    # environment as upper case env. i.e. GIT_USERNAME=<secret_value> 
  - secrets: 
      # The source is the "name:" of a secret within the
      # parent "secrets:" yaml key
      - source: username
      # The target is the desired environment key accessible during
      # the container runtime.
        target: git_username
```

#### The `environment:` key

```yaml
---
steps:
    # Variables to injected into the container environment
    # using a map style syntax.
  - environment:
      DB_NAME: vela
```

```yaml
---
steps:
    # Variables to injected into the container environment
    # using an array style syntax.
  - environment:
      - DB_NAME=vela
```

#### The `ruleset:` key

The following rules can be used to configure a ruleset:

| Name      | Description                                        |
|-----------|----------------------------------------------------|
| `branch`  | name of branch for a build.                        |
| `comment` | pull request comment body.                         |
| `event`   | name of an event for a build.                      |
| `label`   | pull request label.                                |
| `path`    | path to workspace files for a build.               |
| `repo`    | name of the  repo for a build.                     |
| `status`  | name of status for a build.                        |
| `tag`     | name of reference for a build.                     |
| `target`  | name of deployment or schedule target for a build. |

```yaml
---
steps:
  - ruleset:
      # As shown below this step will execute if the build
      # branch is stage or main.
      branch: [ stage, main ]
```

```yaml
---
steps:
  - ruleset:
      # This extends the ability to start new builds through interactions
      # within a pull request. As shown below this will run a step if a “run build”
      # comment is added to the bottom of a pull request.
      comment: [ "run build" ]
```

```yaml
---
steps:
  - name: Event Ruleset
    ruleset:
      # As shown below this step will execute if the build
      # event is push or pull_request. The available events are:
      # comment, push, pull_request, tag, and deployment.
      event: [ push, pull_request ]
  - name: Scope Events
    ruleset:
      # For pull_request and comment events, specifying an action will
      # further scope when the step is executed. These actions include
      # opened, synchronized, and edited for pull_request; created and 
      # edited for comment. To specify an action, use a ":" as shown below.
      event: [pull_request:opened, comment:created]

      # Note: specifying pull_request is the same as 
      # [pull_request:opened, pull_request:synchronized, pull_request:reopened]. 
      # Specifying comment is the same as [comment:created, comment:edited]. 
```

{{% alert color="info" %}}
Event scoping (`event:action`) was included in Vela release `v0.23.0`. As such, general `event` rulesets in pipelines are mapped as following:

- `pull_request` -> [ `pull_request:opened`, `pull_request:synchronize`, `pull_request:reopened` ]
- `comment` -> [ `comment:created`, `comment:edited` ]
- `deployment` -> [ `deployment:created` ]

If you wish to include _all_ event types from an event, you can specify a wildcard at the end:

```yaml
    ruleset:
      event: pull_request*  # will run on opened, reopened, synchronize, edited, labeled, and unlabeled
```

{{% /alert %}}

```yaml
---
steps:
  - name: Labeling a pull request
    ruleset:
      # This step will execute if a pull request has been labeled enhancement.
      event: [ 'pull_request:labeled' ]
      label: [ 'enhancement' ]
  - name: Editing a pull request with labels
    ruleset:
      # This step will execute if a pull request has been edited AND 
      # has the labels enhancement or documentation.
      event: [ 'pull_request:edited' ]
      label: [ 'enhancement', 'documentation' ]
```

```yaml
---
steps:
  - ruleset:
      # As shown below this step will execute if file README.md, any file of type *.md
      # in the root directory or any file in the test/* directory has changed.
      path: [ README.md, "*.md", "test/*" ]
```

```yaml
---
steps:
  - ruleset:
      # As shown below this step will execute if repo exists within the target GitHub
      # organization or the repo is the go-vela/docs repository.
      repo: [ "target/*", "go-vela/docs" ]
```

```yaml
---
steps:
  - ruleset:
      # As shown below this step will execute if the build status is failure or success.
      status: [ failure, success ]
```

```yaml
---
steps:
  - ruleset:
      # As shown below this step will execute if the build ref is dev/* or test/*.
      tag: [ dev/*, test/* ]
```

```yaml
---
steps:
  - ruleset:
      # As shown below this step will execute if the build target is stage or production.
      # This key is only compatible with deployment and schedule events.
      target: [ dev/*, test/* ]
```

The following controls can be used to modify the behavior of the ruleset evaluation:

| Name       | Description                                        | Options                                                                 |
|------------|----------------------------------------------------| ----------------------------------------------------------------------- |
| `continue` | enables continuing the build if the step fails.    | `true`, `false`                                                         |
| `matcher`  | matcher to use when evaluating the ruleset.        | `filepath`, `regexp`                                                    |
| `operator` | operator to use when evaluating the ruleset.       | `and`, `or`                                                             |
| `if`       | limits the step execution to all rules must match. | `branch`, `comment`, `event`, `path`, `repo`, `status`, `tag`, `target` |
| `unless`   | limits the step execution to no rules can match.   | `branch`, `comment`, `event`, `path`, `repo`, `status`, `tag`, `target` |

```yaml
---
steps:
  - ruleset:
      # As shown below this will overwrite Vela's default behavior to
      # allow the build to continue the sequential step pipeline when this step fails.
      continue: true
```

```yaml
---
steps:
  - ruleset:
      # As shown below this will overwrite Vela's default behavior to use a 
      # filepath matcher and instead evaluate all rules with regex. The available
      # matchers are: filepath, and regexp.
      # Note: The regexp matcher uses Go's regexp package. You can find documentation
      # at https://golang.org/pkg/regexp/syntax/
      matcher: regexp
      branch: foo-\\d
```

```yaml
---
steps:
  - ruleset:
      # As shown below this will overwrite Vela's default behavior to use an 
      # "or" behavior when comparing all ruleset rules.
      # The available operators are: and, and or.
      operator: or
```

```yaml
---
steps:
  - ruleset:
      # As shown below this will tell the ruleset to only execute
      # this step when the branch is main and event is push.
      if:
        branch: main
        event: push
```

```yaml
---
steps:
  - ruleset:
      # As shown below this will overwrite Vela's default behavior to tell the ruleset
      # to only execute this step when the branch is not main and event is not push.
      unless:
        branch: main
        event: push
```

#### The `parameters:` key

```yaml
---
steps:
    # Extra configuration variables specific to a plugin. All keys within the 
    # parameters key are injected environment variables into the
    # container as PARAMETER_<KEY_NAME>.
    # As shown below this step will execute a plugin that needs two fields:
    # PARAMETER_REGISTRY=index.docker.io
    # PARAMETER_REPO=octocat/hello-world,go-vela/docs
  - parameters:
      registry: index.docker.io
      repo: [ go-vela/hello-world,  go-vela/docs ]
```

#### The `commands:` key

```yaml
---
steps:
    # Execution instructions to run inside the container. 
  - entrypoint:
      - echo "Hello, World"
```

#### The `template:` key

The following keys can be used to configure a template injection:

| Name   | Description                            |
|--------| ---------------------------------------|
| `name` | Name of template to inject in the step |
| `vars` | Variables injected into the template   |

```yaml
---
steps:
  - template:
      # Name of template to inject in the step. The name must map
      # to an existing template in the parent "template" key.
      name: example
```

```yaml
---
steps:
  - template:
      # Variables injected into the template. Variables can be any
      # primitive or complex YAML types but the corresponding template
      # needs to understand how those templates are to be used.
      vars:
        tags: [ latest, "1.14", "1.15" ]
        pull_policy: always
        commands:
          test: "go test ./..."
          build: "go build ./..."  
```

#### The `report_as` key

```yaml
---
steps:
  # publish custom status for commit with `test suite` as the context
  - report_as: test suite
```

{{% alert color="info" %}}
A pipeline can have up to 10 steps that report their own status.
{{% /alert %}}

#### The `entrypoint:` key

```yaml
---
steps:
    # Commands to execute inside the container.
  - entrypoint:
      - /bin/pwd
      - /bin/ls
```

#### The `detach:` key

```yaml
---
steps:
    # Run the container in a detached (headless) state. Similar to the 
    # "services:" key this will create a container that can be used throughout
    # the duration of the pipeline.
  - detach: true
```

#### The `ulimits:` key

```yaml
---
steps:
    # Set the user limits for the container.  
  - ulimits:
      - name: foo
        soft: 1024
      - name: bar
        soft: 1024
        hard: 2048
```

#### The `user:` key

```yaml
---
steps:
    # Run the container with the foo user.
  - user: foo
```

