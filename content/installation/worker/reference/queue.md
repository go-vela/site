---
title: "Queue"
linkTitle: "Queue"
description: >
  This section contains information on the queue component for the worker.
---

This component is responsible for integrating with a queue system based off the configuration provided.

The queue system is used by Vela for pulling workloads, provided by the [server](/docs/installation/server/), that will be run.

Workloads fetched from the queue are managed with a [first in, first out (FIFO)](https://en.wikipedia.org/wiki/FIFO_(computing_and_electronics)) strategy.

## Configuration

The following options are used to configure the component:

| Name                | Description                                       | Required | Default    | Environment Variables                           |
| ------------------- | ------------------------------------------------- | -------- | ---------- | ----------------------------------------------- |
| `queue.cluster`     | configures the client for a queue cluster         | `false`  | `false`    | `QUEUE_CLUSTER`<br>`VELA_QUEUE_CLUSTER`         |
| `queue.driver`      | type of client to control and operate queue       | `true`   | `N/A`      | `QUEUE_DRIVER`<br>`VELA_QUEUE_DRIVER`           |
| `queue.pop.timeout` | timeout for requests that pop items off the queue | `true`   | `60s`      | `QUEUE_POP_TIMEOUT`<br>`VELA_QUEUE_POP_TIMEOUT` |
| `queue.routes`      | unique channels or topics for pulling workloads   | `true`   | `[ vela ]` | `QUEUE_ROUTES`<br>`VELA_QUEUE_ROUTES`           |

{{% alert title="Note:" color="primary" %}}
For more information on these configuration options, please see the [worker reference](/docs/installation/worker/reference/).
{{% /alert %}}

## Drivers

The following drivers are available to configure the component:

| Name    | Description                               | Documentation     |
| ------- | ----------------------------------------- | ----------------- |
| `redis` | uses a Redis queue for managing workloads | https://redis.io/ |

### Redis

From the [Redis official website](https://redis.io/):

> Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache, and message broker. Redis provides data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes, and streams. Redis has built-in replication, Lua scripting, LRU eviction, transactions, and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster.

The below configuration displays an example of starting the Vela worker that will connect to a Redis queue:

```diff
$ docker run \
  --detach=true \
+ --env=VELA_QUEUE_DRIVER=redis \
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