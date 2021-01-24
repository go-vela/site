---
title: "Anatomy"
linkTitle: "Anatomy"
description: >
  Starlark template anatomy.
---

## Anatomy

In order to make Starlark work with Vela's templates functionality we did have to make a few design decisions on behalf of the users.

### All templates must contain a main that returns the pipeline

This is illustrated in the below example with a starlark file that contains a `def main(ctx)` and returns the data structure that is a valid pipeline.

```python
def main(ctx):
  return {
    'version': '1',
    'steps': [
      {
        'name': 'build',
        'image': golang:latest,
        'commands': [
          'go build',
          'go test',
        ]
      },
    ],
}
```

### Context is used by the compiler to pass information to the template

The compiler will inject user variables defined in the parent template and compile time platform variables. Both sets of variables are injected into the context within a dictionary structure.

#### Platform variables

Syntax: `ctx['vela']['<resource>']['<name>']`

```python
def main(ctx):
  repo = ctx["vela"]["repo"]["full_name"]

  return {
    'version': '1',
    'steps': [
      {
        'name': 'build',
        'image': golang:latest,
        'commands': [
          "go build %s" %, repo,
          'go test',
        ]
      },
    ],
}
```

#### Template variables

Syntax: `ctx['vars'][<name>]`

```python
def main(ctx):
  image = ctx['vars']['image']

  return {
    'version': '1',
    'steps': [
      {
        'name': 'build',
        'image': image,
        'commands': [
          'go build',
          'go test',
        ]
      },
    ],
}
```
