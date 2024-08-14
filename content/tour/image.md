---
title: "Image"
linkTitle: "Image"
weight: 2
description: >
  Learn about images.
---
All Vela steps will require an image declaration to be provided.

The `image:` key is a key component that defines the [Docker Image](https://docs.docker.com/engine/docker-overview/#images) you want to be executed during the step.

The default behavior is for a Vela worker to pull an image if it is not present on the host. Docker daemon's cache image layers locally, by allowing the default behavior to use the cache you can get the advantage of faster build start up times.

Sometimes this isn't the desired behavior and you want the image to always be pulled or pulled at a specific point in the pipeline lifecycle.

That's when you can use the `pull:` key to set the policy for how/when the image pull interaction should be treated.

**Expand your knowledge with an example!**

* [Pull policy](/docs/usage/pull_policies/)

<!-- section break -->

```yaml
# All the below syntaxes would pull an image.
image: alpine
image: alpine:latest
image: alpine:3
image: library/alpine:3
image: index.docker.io/library/alpine
image: index.docker.io/library/alpine:3
```

```yaml
# This is telling Vela to pull the image at the beginning of the pipeline always.
- name: always pull the image
  image: alpine
  pull: always
  commands:
    - echo "Welcome to the Vela docs"

# This is telling Vela to pull the image just before executing the step
- name: pull the image on start
  image: alpine
  pull: on_start
  commands:
    - echo "Welcome to the Vela docs"    
```

<!-- section break -->

**Key references:**

[`name:`](/docs/reference/yaml/steps/#the-name-key), [`image:`](/docs/reference/yaml/steps/#the-image-key), [`pull:`](/docs/reference/yaml/steps/#the-commands-key),  [`commands:`](/docs/reference/yaml/steps/#the-commands-key),

