---
title: "Templates"
linkTitle: "Templates"
weight: 11
description: >
  Learn about template pipelines.
---

Templates help to create reusable workflows in order to make grouping tasks like building and deploying code.

Templates can solve duplicative tasks in a single workflow or be leveraged any number of pipelines to make reusable tasks across multiple workflows.

In this pipeline each step is shown with the minimum required YAML tags to execute a step. 

Both steps are pulling a [Alpine Linux](https://alpinelinux.org/) image from [Docker Hub](https://hub.docker.com/) and executing echo statements.  

<!-- section break -->

```yaml
version: "1"

templates:
  - name: sample
    source: github.com/<org>/<repo>/path/to/file/<template>.yml
    type: github

steps:
  - name: Test versions
    template:
      name: sample
      vars:
        images: [ golang:1.16, golang:1.15, golang:1.14 ]

  - name: Build binary
    image: alpine
    commands:
      - echo "Hello, World"        
```

<!-- section break -->

**Tag references:**

[`templates:`](/docs/reference/yaml/templates), [`vars:`](/docs/reference/yaml/steps/#the-template-tag), 