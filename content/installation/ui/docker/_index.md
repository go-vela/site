---
title: "Docker"
linkTitle: "Docker"
weight: 2
description: >
  This section contains information on deploying the Vela UI service with Docker.
---

## Prerequisites

This section provides all required dependencies to install and start the UI with Docker.

### Dependency 1: Docker

[Docker](https://docs.docker.com/) will be used for downloading the UI and managing the lifecycle of the application.

You can refer to [Docker's official documentation](https://docs.docker.com/get-docker/) on installing and configuring the service.

## Installation

This section provides an example of installing the UI with Docker.

This example only shows a subset of all possible configuration options.

### Step 1: Download the Image

Download the [Docker image](https://docs.docker.com/get-started/overview/#images) for the Vela UI from [DockerHub](https://hub.docker.com/).

You can use the [`docker pull` command](https://docs.docker.com/engine/reference/commandline/pull/) to download the image:

```shell
$ docker pull target/vela-ui:latest
```

{{% alert title="Note:" color="primary" %}}
The `latest` tag will ensure you install the most-recent version of the Vela UI.

To see the full list of available versions, please refer to [the official registry](https://hub.docker.com/r/target/vela-ui).
{{% /alert %}}

### Step 2: Start the UI

Start the Vela UI as a [Docker container](https://docs.docker.com/get-started/overview/#containers) that is configured via environment variables.

You can use the [`docker run` command](https://docs.docker.com/engine/reference/commandline/run/) to start the worker:

```shell
$ docker run \
  --detach=true \
  --env=VELA_API=https://vela-server.example.com \
  --name=ui \
  --publish=80:80 \
  --publish=443:443 \
  --restart=always \
  target/vela-ui:latest
```

{{% alert title="Note:" color="primary" %}}
For a full list of configuration options, please see the [UI reference](/docs/installation/ui/reference/).
{{% /alert %}}

### Step 3: Verify the UI Logs

Ensure the UI started up successfully and is running as expected by inspecting the logs.

You can use the [`docker logs` command](https://docs.docker.com/engine/reference/commandline/logs/) to verify the logs:

```shell
$ docker logs ui
```