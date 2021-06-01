---
title: "Managing Deployments"
toc: true
description: >
  Learn about how to leverage deployments for your builds
---

Pipelines can be written with your specific branching methodology in mind but when it comes to deployments you often want to be very intentional with triggering a change. For this reason, Vela has deployments, a unique build event that is triggered directly via Vela on a specific ref (branch, SHA, tag).

Vela leverages a deep integration with [GitHub Deployments](https://docs.github.com/en/rest/reference/repos#deployments) which will not only trigger your build but create a system of record on GitHub for your deployment action. You can leverage a deployment in your steps like:

{{% alert title="Tip:" color="info" %}}
Make sure you have events enabled on your repo and any secrets are available for that event.
{{% /alert %}}

```yaml
# A step triggering on "all" deployment events
- name: All deployments
  image: alpine
  commands:
    - echo "Running your deployment!"
  ruleset:
    events: [ deployment ]

# A step triggering deployment to a specific target.
# Targets can be any value i.e. dev, stage, eng, prod, etc
- name: Targeted deployments
  image: alpine
  commands:
    - echo "Running deployment for ${VELA_DEPLOYMENT}!"
  ruleset:
    events: [ deployment ]
    target: [ dev, eng ]
```

## Usage

Let us look at an example workflow for executing a deployment on your repo. You should understand the following concepts before proceeding:

* [Steps](/docs/tour/steps/)
  * [image](/docs/tour/image/)
  * [Commands](/docs/tour/environment/)
  * [Ruleset](/docs/tour/ruleset/)

```yaml
version: "1"
steps:
  # A step triggering on "all" deployment events
  - name: All deployments
    image: alpine
    commands:
      - echo "Running your deployment!"
    ruleset:
      events: [ deployment ]

  # A step triggering deployment to a specific target.
  # Targets can be any value i.e. dev, stage, eng, prod, etc
  - name: Targeted deployments
    image: alpine
    commands:
      - echo "Running deployment for ${VELA_DEPLOYMENT}!"
    ruleset:
      events: [ deployment ]
      target: [ dev, eng ]

  # Now that we know how to control a deployment, lets look
  # at adding custom parameters. Sometimes not only do you need
  # control of the target but you want custom data available
  # when your pipeline runs.
  - name: Custom parameters deployments
    image: alpine
    commands:
      - echo "Custom parameter message, ${DEPLOYMENT_PARAMETER_MESSAGE}"
    ruleset:
      events: [ deployment ]
      target: [ dev, eng ]
```

The following CLI commands will trigger the pipeline and produce different permutations of the pipeline executing:

```sh
# Trigger deployment with no additional configuration
$ vela add deployment --org github --repo octocat

# Trigger deployment for a repository with a specific target environment.
$ vela add deployment --org github --repo octocat --target stage

# Add a deployment for a repository with two parameters.
$ vela add deployment --org github --repo octocat --parameter 'message=Hello, custom var!'
```

