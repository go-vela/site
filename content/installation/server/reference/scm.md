---
title: "SCM"
linkTitle: "SCM"
weight: 6
description: >
  This section contains information on the scm component for the Vela server.
---

This component is responsible for integrating with a source control management (SCM) system based off the configuration provided.

The SCM system is used by Vela for both authentication and authorization of interactions performed within the application.

![Authentication Workflow](/docs/installation/server/reference/authentication_workflow.png)

## Configuration

The following options are used to configure the component:

| Name               | Description                                                     | Required | Default                                                  | Environment Variables                         |
| ------------------ | --------------------------------------------------------------- | -------- | -------------------------------------------------------- | --------------------------------------------- |
| `scm.addr`         | fully qualified url for the SCM                                 | `true`   | `https://github.com`                                     | `SCM_ADDR`<br>`VELA_SCM_ADDR`                 |
| `scm.client`       | client ID from the generated OAuth application on the SCM       | `true`   | `N/A`                                                    | `SCM_CLIENT`<br>`VELA_SCM_CLIENT`             |
| `scm.context`      | message to set in commit status on the SCM                      | `true`   | `continuous-integration/vela`                            | `SCM_CONTEXT`<br>`VELA_SCM_CONTEXT`           |
| `scm.driver`       | type of client to control and operate SCM                       | `true`   | `github`                                                 | `SCM_DRIVER`<br>`VELA_SCM_DRIVER`             |
| `scm.scopes`       | permission scopes to apply for the OAuth credentials on the SCM | `true`   | `[ repo, repo:status, user:email, read:user, read:org ]` | `SCM_SCOPES`<br>`VELA_SCM_SCOPES`             |
| `scm.secret`       | client secret from the generated OAuth application on the SCM   | `true`   | `N/A`                                                    | `SCM_SECRET`<br>`VELA_SCM_SECRET`             |
| `scm.webhook.addr` | url for webhooks on the SCM to send requests to                 | `false`  | the address of the Vela server (`$VELA_ADDR`)            | `SCM_WEBHOOK_ADDR`<br>`VELA_SCM_WEBHOOK_ADDR` |

{{% alert title="Note:" color="primary" %}}
For more information on these configuration options, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}

## Drivers

The following drivers are available to configure the component:

| Name     | Description                                           | Documentation             |
| -------- | ----------------------------------------------------- | ------------------------- |
| `github` | uses a GitHub or GitHug Enterprise Server for the SCM | https://github.com/about/ |

### GitHub

From the [GitHub official website](https://github.com/about/):

> GitHub is where the world builds software. Millions of developers and companies build, ship, and maintain their software on GitHub—the largest and most advanced development platform in the world.

The below configuration displays an example of creating a [GitHub OAuth application](https://docs.github.com/developers/apps/building-oauth-apps/creating-an-oauth-app):

![OAuth Application](/docs/installation/server/github_oauth.png)

{{% alert title="Warning:" color="secondary" %}}
The `Homepage URL` should match [the `VELA_ADDR` environment variable](/docs/installation/server/reference/#vela_addr) provided to the server for clusters without a UI.

Otherwise, the `Homepage URL` should match [the `VELA_WEBUI_ADDR` environment variable](/docs/installation/server/reference/#vela_webui_addr) provided to the server.

The `Authorization callback URL` should contain [the `VELA_ADDR` environment variable](/docs/installation/server/reference/#vela_addr) with a `/authenticate` suffix.
{{% /alert %}}

### GitHub Enterprise Server

From the [GitHub Enterprise official website](https://docs.github.com/en/enterprise-server/admin/overview/system-overview):

> GitHub Enterprise Server is your organization's private copy of GitHub contained within a virtual appliance, hosted on premises or in the cloud, that you configure and control.

The below configuration displays an example of creating a [GitHub Enterprise Server OAuth application](https://docs.github.com/enterprise-server@3.3/developers/apps/building-oauth-apps/creating-an-oauth-app):

![OAuth Application](/docs/installation/server/github_enterprise_oauth.png)

{{% alert title="Warning:" color="secondary" %}}
The `Homepage URL` should match [the `VELA_ADDR` environment variable](/docs/installation/server/reference/#vela_addr) provided to the server for clusters without a UI.

Otherwise, the `Homepage URL` should match [the `VELA_WEBUI_ADDR` environment variable](/docs/installation/server/reference/#vela_webui_addr) provided to the server.

The `Authorization callback URL` should contain [the `VELA_ADDR` environment variable](/docs/installation/server/reference/#vela_addr) with a `/authenticate` suffix.
{{% /alert %}}