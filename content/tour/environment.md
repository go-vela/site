---
title: "Environment"
linkTitle: "Environment"
weight: 4
description: >
  Learn about environment.
---

To define environment variables scoped to a step you can add an `environment:` YAML tag.

Every step's environment is isolated to each individual step and all platform variables get injected with a custom `VELA_` prefix pattern.

Vela does import a library to provide partial string operations. You can use the functions to manipulate string values prior to substitution.

With this substitution you should be aware `${variable}` expressions are subject to pre-processing. If you want to avoid this behavior you can escape your expressions to avoid the pre-processor evaluations.

**Expand your knowledge with an example!**

* [Using the environment](/docs/usage/environment/)

<!-- section break -->

```yaml
- name: Vela Platform ENV
  image: alpine
  commands:
    - echo ${VELA_REPO_FULL_NAME}

- name: Custom User ENV
  image: alpine
  environment:
    MESSAGE: Hello, World
  commands:
    - echo ${MESSAGE}

- name: String Operation
  image: alpine
  commands:
    # This ":0:8" shorthand will cut the value of the commit
    # down to just the first 0 through 8 characters of the sha.
    - echo ${VELA_BUILD_COMMIT:0:8}    
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`environment:`](/docs/reference/yaml/steps/#the-environment-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag), 