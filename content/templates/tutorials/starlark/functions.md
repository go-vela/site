---
title: "Functions"
linkTitle: "Functions"
description: >
  Example Starlark template with functions.
---

{{% alert color="note" %}}
We recommend reviewing [Starlark Spec](https://github.com/bazelbuild/starlark/blob/master/spec.md) before attempting to create a template.
{{% /alert %}}

## Overview

From [Starlark functions](https://github.com/bazelbuild/starlark/blob/master/spec.md#function-definitions):

```star
def twice(x):
    return x * 2

str(twice)              # "<function f>"
twice(2)                # 4
twice("two")            # "twotwo"
```

> The function's name is preceded by the def keyword and followed by the parameter list (which is enclosed in parentheses), a colon, and then an indented block of statements which form the body of the function.

> The parameter list is a comma-separated list whose elements are of four kinds. First come zero or more required parameters, which are simple identifiers; all calls must provide an argument value for these parameters.

> The required parameters are followed by zero or more optional parameters, of the form name=expression. The expression specifies the default value for the parameter for use in calls that do not provide an argument value for it.

> The required parameters are optionally followed by a single parameter name preceded by a *. This is the called the varargs parameter, and it accumulates surplus positional arguments specified by a call.

> Finally, there may be an optional parameter name preceded by **. This is called the keyword arguments parameter, and accumulates in a dictionary any surplus name=value arguments that do not match a prior parameter.

## Sample

Let's take a look at using a function within a template:

```python
def main(ctx):
    return {
        'version': '1',
        'steps': [
            step('foo'),
            step('bar')
        ],
    }

def step(word):
    return {
        "name": "build_%s" % word,
        "image": "alpine:latest",
        'commands': [
            "echo %s" % word
        ]
    }
```

The caller of this template could look like:

```yaml
version: "1"
templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.star
    format: starlark
    type: github

steps:
  - name: echo
    template:
      name: sample
      vars:
```

Which means the compiled pipeline for execution on a worker is:

```yaml
version: 1
steps:
  - name: sample_build_foo
    image: alpine:latest
    commands:
      - echo foo

  - name: sample_build_bar
    image: alpine:latest
    commands:
      - echo bar
```
