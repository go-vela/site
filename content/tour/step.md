---
title: "Step"
linkTitle: "Step"
weight: 1
description: >
  Learn about Step.
---

A step declaration allows you to provide an execution instructions for a pipeline.

The following step is displaying an example of a minimal configuration for executing. 

The `name:` key is the unique identifier for the step throughout the lifecycle of the execution. 

When `commands:` are provided they are converted to a shell script and executed as the Docker entrypoint for the container.

<!-- section break -->

```yaml
- name: Welcome
  image: alpine
  commands:
    - echo "Welcome to the Vela docs"
```

```sh
#!/bin/sh

set -e

echo "Welcome to the Vela docs"

docker run --entrypoint=build.sh alpine:latest
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag), 