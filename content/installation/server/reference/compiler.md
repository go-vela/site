---
title: "Compiler"
linkTitle: "Compiler"
description: >
  This section contains information on the compiler component for the Vela server.
---

{{% alert title="Note:" color="primary" %}}
The compiler is embedded directly in the server and can only be accessed through the server.
{{% /alert %}}

This component is responsible for transforming a [pipeline](/docs/tour/) into an executable representation for the [worker](/docs/installation/worker/).

During the transformation, it will retrieve [templates](/docs/tour/templates/) from one or more registries depending on the pipeline configuration.

By default, Vela will use [GitHub](https://github.com/) as a registry for fetching templates, but you can configure additional registries as well.

However, to fetch templates from a private organization or repository on GitHub, you need to provide a token to the compiler.

Additionally, the compiler can send pipelines to an external endpoint, to be modified, based off custom configuration.

This modification endpoint can be used to perform any number of customizations to all workloads created by the system.

Some examples of what the modification endpoint can do include, but are not limited to:

* injecting or updating the configuration for [secrets](/docs/tour/secrets/) in the pipeline
* injecting or updating the configuration for [services](/docs/tour/services/) in the pipeline
* injecting or updating the configuration for [stages](/docs/tour/stages/) in the pipeline
* injecting or updating the configuration for [steps](/docs/tour/steps/) in the pipeline

## Configuration

The following options are used to configure the component:

| Name                   | Description                                                                     | Required | Default               | Environment Variables                                   |
| ---------------------- | ------------------------------------------------------------------------------- | -------- | --------------------- | ------------------------------------------------------- |
| `clone-image`          | default clone image to use for Vela injected clone step                         | `true`   | `target/vela-git` (1) | `VELA_CLONE_IMAGE`                                      |
| `github-driver`        | enables using Github or GitHub Enterprise Server as a registry for templates    | `false`  | `false`               | `COMPILER_GITHUB`<br>`VELA_COMPILER_GITHUB`             |
| `github-url`           | fully qualified url to GitHub or GitHub Enterprise Server for templates         | `false`  | `N/A`                 | `COMPILER_GITHUB_URL`<br>`VELA_COMPILER_GITHUB_URL`     |
| `github-token`         | token used for authentication when fetching registry templates                  | `false`  | `N/A`                 | `COMPILER_GITHUB_TOKEN`<br>`VELA_COMPILER_GITHUB_TOKEN` |
| `modification-addr`    | fully qualified url to endpoint for modifying pipelines                         | `false`  | `N/A`                 | `MODIFICATION_ADDR`<br>`VELA_MODIFICATION_ADDR`         |
| `modification-retries` | number of times to resend failed requests to the modification endpoint          | `false`  | `5`                   | `MODIFICATION_RETRIES`<br>`VELA_MODIFICATION_RETRIES`   |
| `modification-secret`  | authenticates communication between compiler and the modification endpoint      | `false`  | `N/A`                 | `MODIFICATION_SECRET`<br>`VELA_MODIFICATION_SECRET`     |
| `modification-timeout` | timeout for requests sent to the modification endpoint                          | `false`  | `8s`                  | `MODIFICATION_TIMEOUT`<br>`VELA_MODIFICATION_TIMEOUT`   |

_(1) this will be the latest available, tagged release of `target/vela-git` at the time the server component is released_

{{% alert title="Note:" color="primary" %}}
For more information on these configuration options, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}

## Drivers

The following drivers are available to configure the component:

| Name     | Description                                                    | Documentation                                                               |
| -------- | -------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `github` | uses GitHub or GitHug Enterprise Server as a template registry | https://docs.github.com/en/enterprise-server/admin/overview/system-overview |

### GitHub

From the [GitHub official website](https://github.com/about/):

> GitHub is where the world builds software. Millions of developers and companies build, ship, and maintain their software on GitHub—the largest and most advanced development platform in the world.

The below configuration displays an example of starting the Vela server that will use a GitHub Server as a template registry:

```diff
$ docker run \
  --detach=true \
  --env=VELA_ADDR=https://vela-server.example.com \
+ --env=VELA_COMPILER_GITHUB=true \
+ --env=VELA_COMPILER_TOKEN=<github-personal-access-token> \
+ --env=VELA_COMPILER_URL=https://github.com \
  --env=VELA_DATABASE_ENCRYPTION_KEY=<encryption-key> \
  --env=VELA_QUEUE_DRIVER=redis \
  --env=VELA_QUEUE_ADDR=redis://<password>@<hostname>:<port>/<database> \
  --env=VELA_PORT=443 \
  --env=VELA_SECRET=<shared-secret> \
  --env=VELA_SERVER_PRIVATE_KEY=<private_key> \
  --env=VELA_SCM_CLIENT=<oauth-client-id> \
  --env=VELA_SCM_SECRET=<oauth-client-secret> \
  --env=VELA_WEBUI_ADDR=https://vela.example.com \
  --name=server \
  --publish=80:80 \
  --publish=443:443 \
  --restart=always \
  target/vela-server:latest
```

{{% alert title="Note:" color="primary" %}}
This GitHub configuration is enabled by default and is not necessary to provide in order for Vela to operate.

However, this configuration will enable you to fetch templates from a private organization or repository on GitHub.
{{% /alert %}}

### GitHub Enterprise Server

From the [GitHub Enterprise official website](https://docs.github.com/en/enterprise-server/admin/overview/system-overview):

> GitHub Enterprise Server is your organization's private copy of GitHub contained within a virtual appliance, hosted on premises or in the cloud, that you configure and control.

The below configuration displays an example of starting the Vela server that will use a GitHub Enterprise Server as a template registry:

```diff
$ docker run \
  --detach=true \
  --env=VELA_ADDR=https://vela-server.example.com \
+ --env=VELA_COMPILER_GITHUB=true \
+ --env=VELA_COMPILER_TOKEN=<github-personal-access-token> \
+ --env=VELA_COMPILER_URL=https://git.example.com \
  --env=VELA_DATABASE_ENCRYPTION_KEY=<encryption-key> \
  --env=VELA_QUEUE_DRIVER=redis \
  --env=VELA_QUEUE_ADDR=redis://<password>@<hostname>:<port>/<database> \
  --env=VELA_PORT=443 \
  --env=VELA_SECRET=<shared-secret> \
  --env=VELA_SERVER_PRIVATE_KEY=<private_key> \
  --env=VELA_SCM_CLIENT=<oauth-client-id> \
  --env=VELA_SCM_SECRET=<oauth-client-secret> \
  --env=VELA_WEBUI_ADDR=https://vela.example.com \
  --name=server \
  --publish=80:80 \
  --publish=443:443 \
  --restart=always \
  target/vela-server:latest
```
