---
title: "Reference"
linkTitle: "Reference"
weight: 4
description: >
  This section contains a reference of configuration options for the Vela UI service.
---

## Required

This section contains a list of all variables that must be provided to the UI.

### VELA_API

This variable sets a fully qualified URL to the Vela [server](/docs/administration/server/) address.

The variable should be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable should match [the `VELA_ADDR` variable](/docs/administration/server/reference/#vela_addr) provided to the server.
{{% /alert %}}

## Optional

This section contains a list of all variables that can be provided to the UI.

### NODE_ENV

This variable sets the targeted deployment environment for [node.js](https://nodejs.org/).

Setting this variable to `development` will enable development mode for the service and output verbose logging.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `production`.
{{% /alert %}}

### VELA_DOCS_URL

This variable sets a fully qualified URL to the documentation website for Vela.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `https://go-vela.github.io/docs/`.
{{% /alert %}}

### VELA_FEEDBACK_URL

This variable sets a fully qualified URL to the feedback website for Vela.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `https://github.com/go-vela/ui/issues/new/`.
{{% /alert %}}

### VELA_LOG_BYTES_LIMIT

This variable sets the maximum amount of bytes for logs the UI will attempt to render.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `20000` (2 MB).
{{% /alert %}}

### VELA_MAX_BUILD_LIMIT

This variable sets the maximum amount of concurrent builds a repo is allowed to run.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `30`.

This variable should match [the `VELA_MAX_BUILD_LIMIT` variable](/docs/administration/server/reference/#vela_max_build_limit) provided to the server.
{{% /alert %}}