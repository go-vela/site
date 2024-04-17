---
title: "Substitution"
linkTitle: "Substitution"
description: >
  Learn how to use substitution on environment variables
---

Vela imports a substitution library to provide the ability to expand, or substitute, repository and build metadata to facilitate dynamic pipeline configurations.

## String Operations

| Syntax                          | Example with Output                                           | Description                                                                                              |
| ------------------------------- | ------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `${VAR^}`                       | `VAR=example; echo ${VAR^}`<br>► `Example`                    | Converts the first character of the variable to uppercase                                                |
| `${VAR^^}`                      | `VAR=example; echo ${VAR^^}`<br>► `EXAMPLE`                   | Converts all characters of the variable to uppercase                                                     |
| `${VAR,}`                       | `VAR=EXAMPLE; echo ${VAR,}`<br>► `eXAMPLE`                    | Converts the first character of the variable to lowercase                                                |
| `${VAR,,}`                      | `VAR=EXAMPLE; echo ${VAR,,}`<br>► `example`                   | Converts all characters of the variable to lowercase                                                     |
| `${VAR:position}`               | `VAR=example; echo ${VAR:1}`<br>► `xample`                    | Extracts a substring from the variable starting at the position                                          |
| `${VAR:position:length}`        | `VAR=example; echo ${VAR:2:3}`<br>► `amp`                     | Extracts a substring from the variable starting at the position with the specified length                |
| `${VAR#substring}`              | `VAR=exampleexample; echo ${VAR#exa}`<br>► `mpleexample`      | Removes the shortest match of substring from the start of the variable                                   |
| `${VAR##substring}`             | `VAR=exampleexample; echo ${VAR##*exa}`<br>► `mple`           | Removes the longest match of substring from the start of the variable                                    |
| `${VAR%substring}`              | `VAR=exampleexample; echo ${VAR%mple}`<br>► `exampleexa`      | Removes the shortest match of substring from the end of the variable                                     |
| `${VAR%%substring}`             | `VAR=exampleexample; echo ${VAR%%mple*}`<br>► `exa`           | Removes the longest match of substring from the end of the variable                                      |
| `${VAR/substring/replacement}`  | `VAR=exampleexample; echo ${VAR/exam/ap}`<br>► `appleexample` | Replaces the first match of substring with replacement in the variable                                   |
| `${VAR//substring/replacement}` | `VAR=exampleexample; echo ${VAR//exam/ap}`<br>► `appleapple`  | Replaces all matches of substring with replacement in the variable                                       |
| `${VAR/#substring/replacement}` | `VAR=example; echo ${VAR/#exam/ap}`<br>► `apple`              | If the variable starts with substring, replace it with replacement                                       |
| `${VAR/%substring/replacement}` | `VAR=example; echo ${VAR/%mple/ctly}`<br>► `exactly`          | If the variable ends with substring, replace it with replacement                                         |
| `${#VAR}`                       | `VAR=example; echo ${#VAR}`<br>► `7`                          | Returns the length of the variable                                                                       |
| `${VAR=default}`                | `unset VAR; echo ${VAR=default}`<br>► `default`               | If the variable is unset or null, it will be set to `default`                                            |
| `${VAR:=default}`               | `unset VAR; echo ${VAR:=default}`<br>► `default`              | If the variable is unset or null, it will be set to `default` and the assignment is exported             |
| `${VAR:-default}`               | `unset VAR; echo ${VAR:-default}`<br>► `default`              | If the variable is unset or null, it will be replaced with `default` without changing the value of `VAR` |

{{% alert title="Note" color="info" %}}
If you want to play with the examples above in a terminal, make sure you are in a `bash` shell.
{{% /alert %}}

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
