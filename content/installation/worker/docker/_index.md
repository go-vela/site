---
title: "Docker"
linkTitle: "Docker"
weight: 2
description: >
  This section contains information on deploying the Vela worker service with Docker.
---

## Prerequisites

This section provides all required dependencies to install and start the worker with Docker.

### Dependency 1: Docker

[Docker](https://docs.docker.com/) will be used for downloading the worker and managing the lifecycle of the application.

You can refer to [Docker's official documentation](https://docs.docker.com/get-docker/) on installing and configuring the service.

### Dependency 2: Redis

[Redis](https://redis.io/) will be used for storing workloads, created by the [server](/docs/installation/server/), that will be run by a worker.

You can refer to [Redis's official documentation](https://redis.io/topics/quickstart/) on installing and configuring the service.

## Installation

This section provides an example of installing the worker with Docker.

This example only shows a subset of all possible configuration options.

### Step 1: Download the Image

Download the [Docker image](https://docs.docker.com/get-started/overview/#images) for the Vela worker from [DockerHub](https://hub.docker.com/).

You can use the [`docker pull` command](https://docs.docker.com/engine/reference/commandline/pull/) to download the image:

```shell
$ docker pull target/vela-worker:latest
```

{{% alert title="Note:" color="primary" %}}
The `latest` tag will ensure you install the most-recent version of the Vela worker.

To see the full list of available versions, please refer to [the official registry](https://hub.docker.com/r/target/vela-worker).
{{% /alert %}}

### Step 2: Start the Worker

Start the Vela worker as a [Docker container](https://docs.docker.com/get-started/overview/#containers) that is configured via environment variables.

You can use the [`docker run` command](https://docs.docker.com/engine/reference/commandline/run/) to start the worker:

```shell
$ docker run \
  --detach=true \
  --env=VELA_QUEUE_DRIVER=redis \
  --env=VELA_QUEUE_ADDR=redis://<password>@<hostname>:<port>/<database> \
  --env=VELA_SERVER_ADDR=https://vela-server.example.com \
  --env=VELA_SERVER_SECRET=<shared-secret> \
  --env=VELA_WORKER_ADDR=https://vela-worker.example.com \
  --name=worker \
  --publish=80:80 \
  --publish=443:443 \
  --restart=always \
  --volume=/var/run/docker.sock:/var/run/docker.sock \
  target/vela-worker:latest
```

{{% alert title="Note:" color="primary" %}}
For a full list of configuration options, please see the [worker reference](/docs/installation/worker/reference/).
{{% /alert %}}

### Step 3: Verify the Worker Logs

Ensure the worker started up successfully and is running as expected by inspecting the logs.

You can use the [`docker logs` command](https://docs.docker.com/engine/reference/commandline/logs/) to verify the logs:

```shell
$ docker logs worker
```
