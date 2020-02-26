---
title: "Kubernetes"
---

## Overview

This plugin enables the ability to manage resources in [Kubernetes](https://kubernetes.io/) in a Vela pipeline.

Source Code: https://github.com/go-vela/vela-kubernetes

Registry: https://hub.docker.com/r/target/vela-kubernetes

## Usage

Sample of applying Kubernetes files:

```yaml
steps:
  - name: kubernetes
    image: target/vela-kubernetes:v0.1.0
    pull: true
    parameters:
      action: apply
      files: [ kubernetes/common, kubernetes/dev/deploy.yml ]
```

Sample of pretending to apply Kubernetes files:

```diff
steps:
  - name: kubernetes
    image: target/vela-kubernetes:v0.1.0
    pull: true
    parameters:
      action: apply
+     dry_run: true
      files: [ kubernetes/common, kubernetes/dev/deploy.yml ]
```

Sample of patching containers in Kubernetes files:

```yaml
steps:
  - name: kubernetes
    image: target/vela-kubernetes:v0.1.0
    pull: true
    parameters:
      action: patch
      files: [ kubernetes/common, kubernetes/dev/deploy.yml ]
      containers:
        - name: sample
          image: alpine:latest
```

Sample of pretending to patch containers in Kubernetes files:

```diff
steps:
  - name: kubernetes
    image: target/vela-kubernetes:v0.1.0
    pull: true
    parameters:
      action: patch
+     dry_run: true
      files: [ kubernetes/common, kubernetes/dev/deploy.yml ]
      containers:
        - name: sample
          image: alpine:latest
```

Sample of watching the status of resources:

```yaml
steps:
  - name: kubernetes
    image: target/vela-kubernetes:v0.1.0
    pull: true
    parameters:
      action: status
      statuses: [ sample ]
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.
{{% /alert %}}

Users can use [Vela secrets](/docs/concepts/pipeline/secrets/) to substitute sensitive values at runtime:

```diff
steps:
  - name: kubernetes
    image: target/vela-kubernetes:v0.1.0
    pull: true
+   secrets: [ kube_config ]
    parameters:
      action: apply
      files: [ kubernetes/common, kubernetes/dev/deploy.yml ]
-     config: |
-     ---
-     apiVersion: v1
-     kind: Config
```

## Parameters

The following parameters are used to configure the image:

| Name        | Description                                          | Required | Default           |
| ----------- | ---------------------------------------------------- | -------- | ----------------- |
| `action`    | action to perform against Kubernetes                 | `true`   | `N/A`             |
| `cluster`   | Kubernetes cluster from the configuration file       | `false`  | `N/A`             |
| `context`   | Kubernetes context from the configuration file       | `false`  | `N/A`             |
| `file`      | configuration file for communication with Kubernetes | `true`   | `N/A`             |
| `log_level` | set the log level for the plugin                     | `true`   | `info`            |
| `namespace` | Kubernetes namespace from the configuration file     | `false`  | `N/A`             |
| `path`      | path to Kubernetes configuration file                | `false`  | **set by Vela**   |

#### Apply

The following parameters are used to configure the `apply` action:

| Name      | Description                                      | Required | Default |
| --------- | ------------------------------------------------ | -------- | ------- |
| `dry_run` | enables pretending to perform the apply          | `false`  | `false` |
| `files`   | list of Kubernetes files or directories to apply | `true`   | `N/A`   |
| `output`  | set the output for the apply                     | `false`  | `N/A`   |

#### Patch

The following parameters are used to configure the `patch` action:

| Name         | Description                                      | Required | Default |
| ------------ | ------------------------------------------------ | -------- | ------- |
| `containers` | containers from the files to patch               | `true`   | `N/A`   |
| `dry_run`    | enables pretending to perform the patch          | `false`  | `false` |
| `files`      | list of Kubernetes files or directories to patch | `true`   | `N/A`   |
| `output`     | set the output for the patch                     | `false`  | `N/A`   |

#### Status

The following parameters are used to configure the `status` action:

| Name       | Description                                      | Required | Default |
| ---------- | ------------------------------------------------ | -------- | ------- |
| `statuses` | list of Kubernetes resources to watch status on  | `true`   | `N/A`   |
| `timeout`  | total time allowed to watch Kubernetes resources | `true`   | `5m`    |
| `watch`    | enables watching until the resource completes    | `false`  | `true`  |

## Template

COMING SOON!

## Troubleshooting

Below are a list of common problems and how to solve them:
