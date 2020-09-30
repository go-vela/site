---
title: "Overview"
linkTitle: "Overview"
description: >
  Learn about Templates for Vela.
---

A template is a pipeline with one to many defined steps that can be sourced into another pipeline. Templates can live in any repository in a [source control system](/docs/concepts/infrastructure/server/source/) and are expanded at compile time to create the final executable pipeline.

Templates can take the form of generalized workflows across repositories or complex workflows like matrices in a single build.

{{% alert color="warning" %}}
The following YAML tags are not valid inside a template pipeline:

* `services:`
* `secrets:`
* `stages:`
* `templates:`
{{% /alert %}}

## Template Engines

At this time the only supported template engine is [Go Templates](https://golang.org/pkg/text/template/). We extend Go's built-in template functions by utilizing the [sprig library](http://masterminds.github.io/sprig/) in the engine to allow for more options on top of the Go template syntax.

Let's take a look at a basic template:

{{% alert color="tip" %}}
For this example we will call it build.yml but the YAML does not have a required name.
{{% /alert %}}

```yaml
metadata:
  template: true

steps:
  - name: Test and Build
    commands:
      - go test ./...
      - go build
    image: {{ .image }}
    pull: always
    ruleset:
      event: [ push, pull_request ]
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/octocat/hello-world/.vela/build.yml
    type: github

steps:
  - name: sample
    template:  
      name: golang
      vars:
        image: golang:latest
```
