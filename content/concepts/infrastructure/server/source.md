---
title: "Source"
linkTitle: "Source"
description: >
  This section contains information on the source server component.
---

The `source` component is one of the server components for Vela.

This component defines the system Vela uses for integrating with the source code.

{{% alert color="info" %}}
This system is often referred to as a "version control system" or "source control provider".
{{% /alert %}}

## Configuration

The following options are used to configure the component:

| Name             | Environment      | Description                                       |
| ---------------- | ---------------- | ------------------------------------------------- |
| `source.driver`  | `SOURCE_DRIVER`  | type of client to control and operate source      |
| `source.url`     | `SOURCE_URL`     | full navigatable url to source system             |
| `source.client`  | `SOURCE_CLIENT`  | OAuth client ID for source system                 |
| `source.secret`  | `SOURCE_SECRET`  | OAuth client secret for source system             |
| `source.context` | `SOURCE_CONTEXT` | message to set in commit status for source system |

{{% alert color="info" %}}
All available options support `VELA_*` prefixes for the environment variables. For example:
* `SOURCE_DRIVER` - type of client to control and operate queue
* `VELA_SOURCE_DRIVER` - type of client to control and operate queue
{{% /alert %}}

#### Drivers

The following drivers are available to configure the component:

| Name     | Description                               | Documentation            |
| -------- | ----------------------------------------- | ------------------------ |
| `github` | uses a GitHub instance for source control | https://github.com/about |
| `gitlab` | uses a GitLab instance for source control | https://about.gitlab.com |

{{% alert color="warning" %}}
GitLab is not fully supported. Using GitLab is coming soon!
{{% /alert %}}
