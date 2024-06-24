---
title: "Status"
linkTitle: "Status"
weight: 12
description: >
  Learn about Vela statuses.
---

Vela will always publish build statuses to the source control management system. These statuses correspond with the webhook event that triggered the build.

These statuses can be used to define various branch protection policies.

Vela also supports up to 10 step-level statuses. These statuses will reflect the success or failure of the _step_ rather than the build. The name of this status will match the value of the `report_as` tag.

<!-- section break -->

```yaml
# In this pipeline, the status of the build overall will publish 
# to the source control management system (SCM).
#
# The step "Test Suite" will publish to the
# SCM separately as `<context_prefix>/<event>/testing`.

- name: Welcome
  image: alpine
  commands:
    - echo "Welcome to the Vela docs"

- name: Test Suite
  image: golang:latest
  report_as: testing
  commands:
    - go test
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/steps/#the-name-tag), [`image:`](/docs/reference/yaml/steps/#the-image-tag), [`commands:`](/docs/reference/yaml/steps/#the-commands-tag), [`report_as:`](/docs/reference/yaml/steps/#the-report_as-tag)