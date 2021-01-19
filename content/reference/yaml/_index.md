---
title: "YAML"
linkTitle: "YAML"
layout: reference
description: >
  reference information for creating Vela pipelines
---

Steps and Stages Pipeline use "YAML Ain’t Markup Language" (YAML) which is a data serialization language designed to be human friendly. Vela accepts YAML files with either a `.yml` or `.yaml` extension. If you'd like to learn more about the YAML language, we recommend you see, "[Learn YAML in five minutes.](https://www.codeproject.com/Articles/1214409/Learn-YAML-in-five-minutes)".

{{% alert title="Tip:" color="info" %}}
The design goals for YAML are, in decreasing priority:

1. YAML is easily readable by humans.
2. YAML data is portable between programming languages.
3. YAML matches the native data structures of agile languages.
4. YAML has a consistent model to support generic tools.
5. YAML supports one-pass processing.
6. YAML is expressive and extensible.
7. YAML is easy to implement and use.

See YAML [design goals](https://yaml.org/spec/1.2/spec.html#Introduction) from spec.
{{% /alert %}}

## Terminology Check

Whether you are a YAML expert or a novice here is some quick terminology that is used without the Vela reference documentation you should be aware of:

{{% alert title="Tip:" color="info" %}}
You can get feedback directly on your `.vela.yml` or `.vela.yaml` pipelines in your IDE with the available [JSON Schema](/docs/usage/schema/). 
{{% /alert %}}

### Document

A file ending with `.yml` or `.yaml` that contains contents following the YAML spec is called a document, see [YAML 1.2 spec for full details](https://yaml.org/spec/1.2/spec.html#id2800132).

Example:

```yml
---
key: value
```

### Tags

A YAML document is compose of one to many key-value pairs where the key is called the tag and the value is evaluated to an explicit type (Int, Float, string, bool, etc), see [YAML 1.2 spec for full details](https://yaml.org/spec/1.2/spec.html#id2761292).

Example:

```yml
---
# an integer
canonical: 12345

# a float
canonical: 3.14159e+3

# a string
canonical: "Hello, World"

# a bool
canonical: true
```