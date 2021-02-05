---
title: "Image"
linkTitle: "Image"
weight: 2
description: >
  Learn about images.
---
All Vela steps will require an image declaration to be provided.

The `image:` tag is a key component defines a [Docker Image](https://docs.docker.com/engine/docker-overview/#images) you want to executed during the step.

The default behavior is for a Vela worker component to pull an image if not present. Since the Docker daemon builds up a large cache this had the advantage of executing the build very quickly.

Sometimes this isn't the desired behavior and you want the image to always be pulled or pulled at a specific point in the pipeline lifecycle.

That's when you cant use the `pull:` YAML tag to set the policy on the step for how/when the image should be treated. 



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

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`pull:`](/docs/reference/yaml/steps/#the-commands-tag),  [`commands:`](/docs/reference/yaml/steps/#the-commands-tag), 