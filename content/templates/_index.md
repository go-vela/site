---
title: "Templates"
linkTitle: "Templates"
layout: templates
description: >
  This section contains information on how to use Vela templates.
menu:
  main:
    weight: 405
---

A template is a pipeline with one to many defined steps that can be sourced into another pipeline. Templates can live in any repository in a source control system and are expanded at compile time to create the final executable pipeline.

Templates can take the form of generalized workflows across repositories or complex workflows like matrices in a single build.

{{% alert color="warning" %}}
The following YAML tags are not valid inside a template pipeline:

* `stages:`
* `templates:`
{{% /alert %}}

## Reference documentation

Check out the [YAML reference documentation](/docs/reference/yaml/templates/) for templates.

## Template Engines

### Format

By default, templates utilize the Go template language unless otherwise specified. You may opt to specify the `format` key to switch the template language to one of the following:

* `format: go`
* `format: golang`
* `format: ""`
* `format: starlark`

### Go Template

[Go Templates](https://golang.org/pkg/text/template/) is the default formatter for building out template pipelines. We extend Go's built-in template functions by utilizing the [sprig library](http://masterminds.github.io/sprig/) in the engine to allow for more options on top of the Go template syntax.

Let's take a look at a basic template:

{{% alert title="Tip:" color="info" %}}
For this example we will call it `build.yml` but the YAML does not have a required name.
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
  - name: go
    source: github.com/octocat/hello-world/.vela/build.yml
    format: go
    type: github

steps:
  - name: sample
    template:
      name: go
      vars:
        image: golang:latest
```

### Starlark

[Starlark](https://github.com/bazelbuild/starlark) is a configuration language that was designed for the [Bazel build system](https://bazel.build/). The language is a [Python](https://www.python.org/) dialect that exists for advanced configuration management that can require complex structures. The language is dynamically typed and allows for all sorts of language-esque primitives to make writing large configuration files more manageable.

It is recommended users read the [Starlark Spec](https://github.com/bazelbuild/starlark/blob/master/spec.md) to understand the syntax differences between Python and Starlark. Python IDE tools are compatible with Starlark to assist users in writing their `.star` or `.py` template pipelines.

Let's take a look at a basic template:

{{% alert title="Tip:" color="info" %}}
For this example we will call it `build.star` but the file does not have a required name.
{{% /alert %}}

```python
def main(ctx):
  return {
    'version': '1',
    'steps': [
      {
        'name': 'build',
        'image': ctx["vars"]["image"],
        'commands': [
          'go build',
          'go test',
        ]
      },
    ],
}
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: starlark
    source: github.com/octocat/hello-world/.vela/build.star
    format: starlark
    type: github

steps:
  - name: sample
    template:
      name: starlark
      vars:
        image: golang:latest
```

### Templating directly in `.vela.yml`

As of `0.9.0` Vela allows using Starlark and Go templates directly in the `.vela.yml` 
given you select the desired template language in the pipeline settings `https://vela.company.com/<org>/<repo>/settings`.

**NOTE:** When Starlark is chosen in the pipeline settings, Vela will look for any of the following files for the pipeline instructions
`.vela.yml`, `.vela.py` or `.vela.star`

#### Example `.vela.yml` using Golang
```yaml
version: "1"

# The trailing dash trims any whitespace to the right of the closing }} tag. See
# https://pkg.go.dev/text/template#hdr-Text_and_spaces
{{$stageList := list "foo" "bar" "star" -}}

stages:
  {{range $stage := $stageList -}}
  {{ $stage }}:
    steps:
      - name: {{ $stage }}
        image: alpine
        commands:
          - echo hello from {{ $stage }}
  {{ end }}
```

#### Example `.vela.yml`, `.vela.py` or `.vela.star` using Starlark
```python

def main(ctx):
  stageNames = ["foo", "bar", "star"]

  stages = {}

  for name in stageNames:
    stages[name] = stage(name)

  return {
      'version': '1',
      'stages': stages
  }

def stage(word):
  return {
      "steps": [
        {
          "name": "build_%s" % word,
          "image": "alpine:latest",
          'commands': [
              "echo hello from %s" % word
          ]
        }
      ]
  }
```

### Rendering inline directly in `.vela.yml`

Rendering a template inline gives you the power of:

 - using an external template without the need of having to specify using that directly in the pipeline 
 - merging templates into an existing pipeline without needing to be expanded

{{% alert title="Warning:" color="warning" %}}
You **can not** mix stages and steps pipelines in a single render. They must be all of one type. 
{{% /alert %}}

Using this feat unlocks powerful pipelines that allow you to use templates with:

- stages
- steps
- services
- secrets

To use this feature all you need to do is add `render_inline: true` in the metadata block of your pipeline and you can start compiling templates without the need of the stages and steps blocks. This feature does work with both Go templates and Starlark. 

#### Basic

This example is for injecting a stages into an external calling pipeline.

{{% alert title="Tip:" color="info" %}}
The same pattern can be used with steps workflows.
{{% /alert %}}

```yaml
metadata:
  template: true

stages:
  test:
    steps:
      - name: Test
        commands:
          - go test ./...
        image: {{ .image }}
        pull: always
        ruleset:
          event: [ push, pull_request ]
  build:
    steps:
      - name: Build
        commands:
          - go build
        image: {{ .image }}
        pull: always
        ruleset:
          event: [ push, pull_request ]
```

The caller of this template could look like:

```yaml
version: "1"
metadata:
  render_inline: true

templates:
  - name: go
    source: github.com/octocat/hello-world/.vela/build.yml
    format: go
    type: github
    vars:
      image: golang:latest
```

#### Advanced

This example is for combing stages from an external template into the calling pipeline.

{{% alert title="Tip:" color="info" %}}
The same pattern can be used with steps workflows.
{{% /alert %}}

```yaml
metadata:
  template: true

stages:
  test:
    steps:
      - name: Test
        commands:
          - go test ./...
        image: {{ .image }}
        pull: always
        ruleset:
          event: [ push, pull_request ]
```

The caller of this template could look like:

```yaml
version: "1"
metadata:
  render_inline: true

templates:
  - name: go
    source: github.com/octocat/hello-world/.vela/build.yml
    format: go
    type: github
    vars:
      image: golang:latest

stages:
  build:
    steps:
      - name: Build
        commands:
          - go build
        image: {{ .image }}
        pull: always
        ruleset:
          event: [ push, pull_request ]      
```