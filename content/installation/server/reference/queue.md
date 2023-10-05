---
title: "Queue"
linkTitle: "Queue"
description: >
  This section contains information on the queue component for the Vela server.
---

This component is responsible for integrating with a queue system based off the configuration provided.

The queue system is used by the Vela server for pushing workloads that will be run by a [worker](/docs/installation/worker/).

Workloads published to the queue are managed with a [first in, first out (FIFO)](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)) strategy.

## Configuration

The following options are used to configure the component:

| Name                | Description                                                   | Required | Default    | Environment Variables                           |
| ------------------- | ------------------------------------------------------------- | -------- | ---------- | ----------------------------------------------- |
| `queue.addr`        | full connection string to the queue                           | `true`   | `N/A`      | `QUEUE_ADDR`<br>`VELA_QUEUE_ADDR`               |
| `queue.cluster`     | configures the client for a queue cluster                     | `false`  | `false`    | `QUEUE_CLUSTER`<br>`VELA_QUEUE_CLUSTER`         |
| `queue.driver`      | type of client to control and operate queue                   | `true`   | `N/A`      | `QUEUE_DRIVER`<br>`VELA_QUEUE_DRIVER`           |
| `queue.pop.timeout` | timeout for requests that pop items off the queue             | `true`   | `60s`      | `QUEUE_POP_TIMEOUT`<br>`VELA_QUEUE_POP_TIMEOUT` |
| `queue.routes`      | unique channels or topics for pushing workloads               | `true`   | `[ vela ]` | `QUEUE_ROUTES`<br>`VELA_QUEUE_ROUTES`           |
| `queue.private-key` | private key for signing items prior to push                   | `false`  | `N/A`      | `QUEUE_PRIVATE_KEY`<br>`VELA_QUEUE_PRIVATE_KEY` |
| `queue.public-key`  | public key for opening items after popping them off the queue | `false`  | `N/A`      | `QUEUE_PUBLIC_KEY`<br>`VELA_QUEUE_PUBLIC_KEY`   |

{{% alert title="Note:" color="primary" %}}
For more information on these configuration options, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}

## Drivers

The following drivers are available to configure the component:

| Name    | Description                               | Documentation     |
| ------- | ----------------------------------------- | ----------------- |
| `redis` | uses a Redis queue for managing workloads | https://redis.io/ |

### Redis

From the [Redis official website](https://redis.io/):

> Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache, and message broker. Redis provides data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes, and streams. Redis has built-in replication, Lua scripting, LRU eviction, transactions, and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster.

The below configuration displays an example of starting the Vela server that will connect to a Redis queue:

```diff
$ docker run \
  --detach=true \
  --env=VELA_ADDR=https://vela-server.example.com \
  --env=VELA_DATABASE_ENCRYPTION_KEY=<encryption-key> \
+ --env=VELA_QUEUE_DRIVER=redis \
+ --env=VELA_QUEUE_ADDR=redis://<password>@<hostname>:<port>/<database> \
+ --env=VELA_QUEUE_PRIVATE_KEY=<signing-private-key> \
+ --env=VELA_QUEUE_PUBLIC_KEY=<signing-public-key> \
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