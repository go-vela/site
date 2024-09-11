---
title: "Outputs"
toc: true
description: >
  Learn how to configure outputs for steps.
---

{{% alert title="Tip:" color="info" %}}
Outputs functionality is only available in the Docker runtime.
{{% /alert %}}

### What are outputs and why are they useful?

While the workspace [is shared](/docs/usage/workspace) for all steps in a build, the environment is not. This is because changes to a container environment are not exported after the completion of a step.

For example, take the following pipeline:

```yaml
version: "1"

steps:
    - name: parse image for testing
      image: alpine:latest
      commands:
        # image to use is the first part of the source branch (inventory-updates -> my-organization/inventory:latest)
        - image=$(echo ${VELA_PULL_REQUEST_SOURCE} | sed 's/[_.-].*//')

    - name: test
      image: my-organization/${image}:latest
      pull: on_start
      commands:
        - go test ./...

```

This is not a valid pipeline configuration because `image` will not persist from the first step to the second. However, being able to dynamically update environment variables for substitution or for plugin parameters can be an important part of a CI build.

This is where `outputs` can improve your pipeline configurations.

Let's take the same pipeline but make it valid using outputs:

```yaml
version: "1"

steps:
    - name: parse image for testing
      image: alpine:latest
      commands:
        # image to use is the first part of the source branch (inventory-updates -> my-organization/inventory:latest)
        - echo "image=$(echo ${VELA_PULL_REQUEST_SOURCE} | sed 's/[_.-].*//')" > $VELA_OUTPUTS

    - name: test
      image: my-organization/${image}:latest
      pull: on_start
      commands:
        - go test ./...
```

Writing to `$VELA_OUTPUTS` in environment file format ensures that those key-value pairs persist for the entirety of the build. 

Not only is this more convenient than storing information in the shared workspace, it can also be safer. Vela secrets are masked in logs, but any sensitive value captured during a build has the potential to be leaked in logs if steps or plugins are not configured correctly.

This can be remedied with masked outputs:

```yaml
version: "1"

steps:
    - name: capture API key for testing
      image: alpine:latest
      commands:
        - apk add jq
        - echo "API_KEY=$(curl http://my-test-endpoint/token | jq .token)" > $VELA_MASKED_OUTPUTS

    - name: test
      image: golang:latest
      commands:
        - echo $API_KEY # will print ***
        - go test ./...
```

After the first step is complete, the logs will mask any mention of the `$API_KEY`. 

### Limitations

- Outputs can only be used as environment variables (`$VAR`) or substitution variables (`${VAR}`). Inline Go templating (`{{ .VAR }}`) is done at compile time and will not dynamically be evaluated.

- Masking will only be applied to variables in `$VELA_MASKED_OUTPUTS` in steps that run _after_ the variable has been written. In other words, if `Step A` writes a token to `$VELA_MASKED_OUTPUTS`, `Step A` logs will _not_ mask the value. Only subsequent steps will have the masking applied.