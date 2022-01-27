---
title: "Executor"
linkTitle: "Executor"
description: >
  This section contains information on the executor component for the worker.
---

This component is responsible for coordinating with [the runtime](/docs/administration/worker/runtime/) to manage workload resources.

Throughout the lifecycle of these resources, this component will track and report results back to the [server](/docs/administration/server/).

## Configuration

The following options are used to configure the component:

| Name                    | Description                                       | Required | Default        | Environment Variables                                   |
| ----------------------- | ------------------------------------------------- | -------- | -------------- | ------------------------------------------------------- |
| `executor.driver`       | type of client to control and operate executor    | `true`   | `linux`        | `EXECUTOR_DRIVER`<br>`VELA_EXECUTOR_DRIVER`             |
| `executor.log_method`   | method used to publish logs back to the server    | `true`   | `byte-chunks`  | `EXECUTOR_LOG_METHOD`<br>`VELA_EXECUTOR_LOG_METHOD`     |
| `executor.max_log_size` | maximum log size (in bytes)                       | `false`  | `0` (no limit) | `EXECUTOR_MAX_LOG_SIZE`<br>`VELA_EXECUTOR_MAX_LOG_SIZE` |

{{% alert title="Note:" color="primary" %}}
For more information on these configuration options, please see the [worker reference](/docs/administration/worker/reference/).
{{% /alert %}}

## Drivers

The following drivers are available to configure the component:

| Name    | Description                                            | Documentation          |
| ------- | ------------------------------------------------------ | ---------------------- |
| `linux` | uses a Linux executor for running workloads            | https://www.linux.com/ |
| `local` | uses a Local executor for running workloads (CLI only) | `N/A`                  |

### Linux

From the [Linux official website](https://www.linux.com/what-is-linux/):

> Linux has been around since the mid-1990s and has since reached a user-base that spans the globe. Just like Windows, iOS, and Mac OS, Linux is an operating system. In fact, one of the most popular platforms on the planet, Android, is powered by the Linux operating system.

The below configuration displays an example of starting the Vela worker that will use a Linux executor:

```diff
$ docker run \
  --detach=true \
+ --env=VELA_EXECUTOR_DRIVER=linux \
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
This Linux configuration is enabled by default and is not necessary to provide in order for Vela to operate.
{{% /alert %}}

### Local

The `local` executor driver is only intended for use with the [Vela CLI](/docs/reference/cli/).

It's not recommended to run any workloads on a worker configured with this driver.
