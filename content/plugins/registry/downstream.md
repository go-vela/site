---
title: "Downstream"
---

## Overview

This plugin enables the ability to trigger builds for other repos for [Vela](https://go-vela.github.io/docs/) in a pipeline.

Source Code: https://github.com/go-vela/vela-downstream

Registry: https://hub.docker.com/r/target/vela-downstream

## Usage

{{% alert color="warning" %}}
This plugin will only search up to the last 500 builds in your build history.
{{% /alert %}}

Sample of triggering a downstream build:

```yaml
steps:
  - name: trigger_hello-world
    image: target/vela-downstream:v0.2.0
    pull: true
    parameters:
      branch: master
      repos:
        - octocat/hello-world
      server: https://vela-server.localhost
```

Sample of triggering a downstream build for multiple repos:

```diff
steps:
+  - name: trigger_multiple
-  - name: trigger_hello-world
    image: target/vela-downstream:v0.2.0
    pull: true
    parameters:
      branch: master
      repos:
        - octocat/hello-world
+        - go-vela/hello-world
      server: https://vela-server.localhost
```

Sample of triggering a downstream build for multiple repos with different branches:

{{% alert color="info" %}}
Use the @ symbol at the end of the org/repo to provide a unique branch per repo.
{{% /alert %}}

```diff
steps:
+  - name: trigger_multiple
-  - name: trigger_hello-world
    image: target/vela-downstream:v0.2.0
    pull: true
    parameters:
-      branch: master
      repos:
-        - octocat/hello-world
+        - octocat/hello-world@test
-        - go-vela/hello-world
+        - go-vela/hello-world@stage
      server: https://vela-server.localhost
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.
{{% /alert %}}

The plugin accepts the following `parameters` for authentication:

| Parameter | Environment Variable Configuration                                  |
| --------- | ------------------------------------------------------------------- |
| `token`   | `CONFIG_TOKEN`, `DOWNSTREAM_TOKEN`, `PARAMETER_TOKEN`, `VELA_TOKEN` |

Users can use [Vela secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: trigger_hello-world
    image: target/vela-downstream:v0.2.0
    pull: true
+   secrets: [ downstream_token ]
    parameters:
      branch: master
      repos:
        - octocat/hello-world
      server: https://vela-server.localhost
-     token: superSecretVelaToken
```

{{% alert color="info" %}}
This example will add the `secrets` to the `trigger_hello-world` step as environment variables:

- `DOWNSTREAM_TOKEN`=<value>
{{% /alert %}}

## Parameters

The following parameters are used to configure the image:

| Name        | Description                                      | Required | Default  |
| ----------- | ------------------------------------------------ | -------- | -------- |
| `branch`    | default branch to trigger a build on             | `true`   | `master` |
| `log_level` | set the log level for the plugin                 | `true`   | `info`   |
| `repos`     | list of <org>/<repo> names to trigger a build on | `true`   | `N/A`    |
| `server`    | Vela server to communicate with                  | `true`   | `N/A`    |
| `token`     | token for communication with Vela                | `true`   | `N/A`    |

## Template

COMING SOON!

## Troubleshooting

You can start troubleshooting this plugin by tuning the level of logs being displayed:

```diff
steps:
  - name: trigger_hello-world
    image: target/vela-downstream:v0.2.0
    pull: true
    parameters:
      branch: master
+     log_level: trace
      repos:
        - octocat/hello-world
      server: https://vela-server.localhost
```

Below are a list of common problems and how to solve them:

COMING SOON!
