---
title: "Step"
linkTitle: "Step"
weight: 1
description: >
  Learn about step.
---

A step declaration allows you to provide execution instructions for a pipeline.

The following step is displaying an example of a minimal configuration for executing a simple echo linux command.

The `name:` key is the unique identifier for the step throughout the lifecycle of the execution.

When `commands:` are provided they are converted to a shell script and executed as the Docker entrypoint for the container.

<!-- section break -->

```yaml
# In this step, commands are executed inside the container as the Entrypoint.
# If any command returns a non-zero exit code, the step fails and exits.
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

**Key references:**

[`name:`](/docs/reference/yaml/steps/#the-name-key), [`image:`](/docs/reference/yaml/steps/#the-image-key), [`commands:`](/docs/reference/yaml/steps/#the-commands-key),

