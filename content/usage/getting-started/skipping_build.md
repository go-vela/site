---
title: "Skipping a Build"
linkTitle: "Skipping a Build"
weight: 5
description: >
  Skip builds for certain commits.
---

To prevent Vela from running a build for a commit, add one of the following to your commit title or message:

- `[skip ci]`
- `[ci skip]`
- `[skip vela]`
- `[vela skip]`
- `***no_ci***`

{{% alert title="Note:" color="primary" %}}
You can use upper or lower case.
{{% /alert %}}

Vela will receive the payload from the source control provider and return a 200 response with a reason for why a build was not triggered.