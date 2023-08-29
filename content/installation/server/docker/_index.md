---
title: "Docker"
linkTitle: "Docker"
weight: 2
description: >
  This section contains information on deploying the Vela server service with Docker.
---

## Prerequisites

This section provides all required dependencies to install and start the server with Docker.

### Dependency 1: Docker

[Docker](https://docker.com/) will be used for downloading the server and managing the lifecycle of the application.

You can refer to [Docker's official documentation](https://docs.docker.com/get-docker/) on installing and configuring the service.

### Dependency 2: Redis

[Redis](https://redis.io/) will be used for storing workloads, created by the server, that will run on a [worker](/docs/installation/worker/).

You can refer to [Redis's official documentation](https://redis.io/topics/quickstart/) on installing and configuring the service.

## Installation

This section provides an example of installing the server with Docker.

{{% alert title="Note:" color="primary" %}}
This example only shows a subset of all possible configuration options.
{{% /alert %}}

### Step 1: Download the Image

Download the [Docker image](https://docs.docker.com/get-started/overview/#images) for the Vela server from [DockerHub](https://hub.docker.com/).

You can use the [`docker pull` command](https://docs.docker.com/engine/reference/commandline/pull/) to download the image:

```shell
$ docker pull target/vela-server:latest
```

{{% alert title="Note:" color="primary" %}}
The `latest` tag will ensure you install the most-recent version of the Vela server.

To see the full list of available versions, please refer to [the official registry](https://hub.docker.com/r/target/vela-server).
{{% /alert %}}

### Step 2: Create an Encryption Key

Create an [Advanced Encryption Standard (AES)](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) key used for encrypting sensitive data at rest in the database.

You can use the [`openssl` command](https://www.openssl.org/) to generate the AES key:

```shell
$ openssl aes-128-cbc -k secret -P -md sha1
```

{{% alert title="Note:" color="primary" %}}
This command will output multiple key/value pairs for the AES key.

The specific value we need from the output is the line with `key` in it (i.e. `key=<value>`).
{{% /alert %}}

### Step 3: Create a Shared Secret

{{% alert title="Note:" color="primary" %}}
Skip this step if you are utilizing the [worker registration auth flow](/docs/installation/worker/docker/#worker-registration-and-auth-refresh)
{{% /alert %}}

Create a shared secret used for authenticating communication between workers and the server.

You can use the [`openssl` command](https://www.openssl.org/) to generate the shared secret:

```shell
$ openssl rand -hex 16
```

### Step 4: Create the private key

Create a private key used for minting and validating user, worker auth, and build JWT tokens.

You can also use the [`openssl` command](https://www.openssl.org/) to generate the key.

```shell
$ openssl rand -hex 16
```

### Step 5: Create the signing key pair

Create a key pair (ed25519) used for signing queue items. Items are signed via private key and opened via public key in the server and worker, respectively. The key pair must be base64 encoded prior to being supplied to the server (and worker).

To make it easier, you can use this [Go Playground program](https://go.dev/play/p/-go_7SnJbnP) to generate an encoded key pair that is ready to use.

{{% alert title="Notes:" color="primary" %}}
The private key is used to sign items in the server.
The public key is used to open items in the worker.
Therefore if you've followed the worker installation docs then you may have already generated the private key to use in the server.
{{% /alert %}}

### Step 6: Create an OAuth Application

Vela requires OAuth application credentials from a source control management (SCM) provider.

These credentials are used to authenticate and authorize actions preformed within the platform.

Vela has support for many Source Control Management (SCM) providers to enable the preferences of you and your team.

You can follow the [SCM reference](/docs/installation/server/reference/scm/) for instructions on creating the OAuth application.

### Step 7: Start the Server

Start the Vela server as a [Docker container](https://docs.docker.com/get-started/overview/#containers) that is configured via environment variables.

You can use the [`docker run` command](https://docs.docker.com/engine/reference/commandline/run/) to start the server:

```shell
$ docker run \
  --detach=true \
  --env=VELA_ADDR=https://vela-server.example.com \
  --env=VELA_DATABASE_ENCRYPTION_KEY=<encryption-key> \
  --env=VELA_QUEUE_DRIVER=redis \
  --env=VELA_QUEUE_ADDR=redis://<password>@<hostname>:<port>/<database> \
  --env=VELA_QUEUE_PRIVATE_KEY=<signing-private-key> \
  --env=VELA_PORT=443 \
  --env=VELA_SERVER_PRIVATE_KEY=<private-key> \
  --env=VELA_SCM_CLIENT=<oauth-client-id> \
  --env=VELA_SCM_SECRET=<oauth-client-secret> \
  --env=VELA_WEBUI_ADDR=https://vela.example.com \
  --name=server \
  --publish=80:80 \
  --publish=443:443 \
  --restart=always \
  target/vela-server:latest
```

{{% alert title="Notes:" color="primary" %}}
If using the [server-worker trusted symmetric auth method](/docs/installation/worker/docker/#worker-server-trusted-symmetric-token), be sure to add the `VELA_SECRET` env variable:
```shell
  --env=VELA_SECRET=<shared_secret>
```
For a full list of configuration options, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}

### Step 8: Verify the Server Logs

Ensure the server started up successfully and is running as expected by viewing the logs.

You can use the [`docker logs` command](https://docs.docker.com/engine/reference/commandline/logs/) to inspect the logs:

```shell
$ docker logs server
```

### Step 9: Install Workers

After the server is up and running, you need to install workers to run workloads.

Please refer to [the worker installation docs](/docs/installation/worker/) for more information.