---
title: "Substitution"
linkTitle: "Substitution"
description: >
  Learn how to use substitution on environment variables
---

Vela imports a substitution library to provide the ability to expand, or substitute, repository and build metadata to facilitate dynamic pipeline configurations.

## String Operations

| Syntax                          | Description |
| ------------------------------- | ----------- |
| `${var^}`                       | var substitution with uppercase first char |
| `${var^^}`                      | var substitution with all uppercase        |
| `${var,}`                       | var substitution with lowercase first char |
| `${var,,}`                      | var substitution with all lowercase        |
| `${var:position}`               | var substitution with substring            |
| `${var:position:length}`        | var substitution with substring and length |
| `${var#substring}`              | var substitution with find and replace     |
| `${var##substring}`             | var substitution with find and replace     |
| `${var%substring}`              | var substitution with find and replace     |
| `${var%%substring}`             | var substitution with suffix removal       |
| `${var/substring/replacement}`  | var substitution with find and replace     |
| `${var//substring/replacement}` | var substitution with find and replace     |
| `${var/#substring/replacement}` | var substitution with find and replace     |
| `${var/%substring/replacement}` | var substitution with find and replace     |
| `${#var}`                       | var substitution                           |
| `${var=default}`                | var substitution with default              |
| `${var:=default}`               | var substitution with default              |
| `${var:-default}`               | var substitution with default              |

### Escaping

{{% alert title="Tip:" color="info" %}}
var expressions are evaluated before the yaml is parsed. If you do not want the system to evaluate an expression it must be escaped.
{{% /alert %}}

```diff
version: "1"
steps:
  - name: echo
    commands:
    # This expression does not escape the evaluation
+   - echo ${VELA_BUILD_COMMIT}
    # This expression does escape the evaluation by adding the double '$$'
+   - echo $${VELA_BUILD_COMMIT}
```