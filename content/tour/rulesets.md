---
title: "Rulesets"
linkTitle: "Rulesets"
weight: 3
description: >
  Learn about rulesets.
---

The ruleset allows you to provide conditions to limit the execution of the container.

When you push your code to a source control management system a payload is sent to Vela.

Within that payload contains characteristics about what just happened. Maybe it was a push to the main branch, feature branch or tag on any specific commit.

The ruleset tag gives you the ability to add conditions on the step to tell Vela when this step should be executed.

<!-- section break -->

```yaml
- name: Welcome
  # This ruleset would scope the step to only executing
  # under the conditions a push to the main branch occurred
  ruleset:
    event: push
    branch: main
  image: alpine
  commands:
    - echo "Welcome to the Vela docs"
```

```yaml
- name: Welcome
  # This ruleset would scope the step to never executing
  # under the conditions a push to the main branch occurred
  ruleset:
    unless:
      event: push
      branch: main
  image: alpine
  commands:
    - echo "Welcome to the Vela docs"
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`ruleset:`](/docs/reference/yaml/steps/#the-ruleset-tag),[`image:`](/docs/reference/yaml/steps/#the-image-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag),
