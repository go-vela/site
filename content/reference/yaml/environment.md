---
title: "Environment"
linkTitle: "Environment"
weight: 1
description: >
  YAML tags for environment block
---

The environment tag is intended to be used to inject a global environment configuration into steps, services and secret containers. Control of which container types get the injected environment settings is available via the metadata block.

```yaml
---
# This document is displaying using the environment tag with a map syntax.
# Additionally, you can also use array syntax where the items in
# they array are of pattern HELLO="Hello, Vela!"
environment:
  HELLO: "Hello, Vela!"
```