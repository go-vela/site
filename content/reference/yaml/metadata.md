---
title: "Metadata"
linkTitle: "Metadata"
weight: 2
description: >
  YAML tags for metadata block
---

The metadata tag is intended to be used during the compile phase to signal how to treat the YAML document.

```yaml
---
# This document is displaying all the available tags
# in their default state for the compile process.
metadata:
  template: false
  clone: true
```

## Tags

| Tag        | Required | Type | Description                                   |
|------------|----------|------|-----------------------------------------------|
| `template` | Y        | bool | Enables compiling the pipeline as a template. |
| `clone`    | N        | bool | Enables injecting the default clone process.  |

### Usage

#### The `template:` tag

{{% alert title="Tip:" color="info" %}}
To learn how to write templates, see the [template documentation](/docs/templates).
{{% /alert %}}

```yaml
---
metadata:
  # Enables compiling the pipeline as a template. This value 
  # is defaulted during the compile phase to "false" if not 
  # explicitly provided by the user.
  template: true
```

#### The `clone:` tag

```yaml
---
metadata:
  # Enables injecting the default clone process
  clone: true
```

#### The `environment:` tag

```yaml
---
metadata:
  # By default, the below is populated into every pipeline with
  # services, steps, and secrets. But, when the block exists the
  # configuration specified is used during compile phase.
  environment: [ steps, services, secrets ]
```
