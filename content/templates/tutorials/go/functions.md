---
title: "Functions"
linkTitle: "Functions"
description: >
  Built-in and custom functions available in Go templates.
---

{{% alert color="note" %}}
We recommend reviewing [Go Templates documentation](https://golang.org/pkg/text/template/) before attempting to create a template.

If you're new to YAML we also recommend reviewing the [YAML 1.2 spec](https://yaml.org/spec/1.2/spec.html) for validation on syntax.
{{% /alert %}}

## Overview

Go provides a limited set of built-in template functions. Vela provides a number of additional, predefined functions to utilize in templates.

### Built-in Functions

See [Go template Functions](https://pkg.go.dev/text/template#hdr-Functions) for a list of built-in functions.

#### Example

A function call:
```go-text-template
{{ printf "%q" "output" }}
```

A function call whose final argument comes from the previous command:
```go-text-template
{{ "output" | printf "%q" }}
```

### Custom Functions

#### Sprig

Sprig provides over 100 additional template functions. [Please refer to the original Sprig function documentation](https://masterminds.github.io/sprig/).

To note, the `env` and `expandenv` functions are not available in Vela.

#### toYaml

The `toYaml` function is intended to ease working with passing and rendering YAML content in Vela templates.

##### Example

`.vela.yml`
```yaml
version: "1"
templates:
  - name: golang
    source: github.com/<org>/<repo>/path/to/file/<template>.yml
    type: github

steps:
  - name: sample
    template:
      name: golang
      vars:
        ruleset:
          event: [ push, pull_request ]
          branch: [ main ]
```

`github.com/<org>/<repo>/path/to/file/<template>.yml`
```go-text-template
metadata:
  template: true

steps:
  - name: install
    commands:
      - test
    image: alpine
    ruleset:
      {{- toYaml .ruleset | nindent 6 }}
```

With the pipeline and template above in place, the final resulting pipeline would render as follows:

```yaml
version: "1"
steps:
  - name: sample_install
    commands:
      - test
    image: alpine
    ruleset:
      event: [ push, pull_request ]
      branch: [ main ]
```

#### vela

The `vela` function provides the convenience of accessing [Vela environment variables](/docs/reference/environment/variables/) within your Vela templates. See its dedicated [platform vars page](/docs/templates/tutorials/go/vars_platform/) for more info.

