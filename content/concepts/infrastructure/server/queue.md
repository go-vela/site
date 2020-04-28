---
title: "Queue"
linkTitle: "Queue"
description: >
  This section contains information on the queue server component.
---

The `queue` component is one of the server components for Vela.

This component defines the system Vela uses for publishing workloads to be completed by a [worker](/docs/concepts/infrastructure/worker/).

## Configuration

The following options are used to configure the component:

| Name            | Environment     | Description                                 |
| --------------- | --------------- | ------------------------------------------- |
| `queue.driver`  | `QUEUE_DRIVER`  | type of client to control and operate queue |
| `queue.config`  | `QUEUE_CONFIG`  | full connection string to queue             |
| `queue.cluster` | `QUEUE_CLUSTER` | configures the client for a queue cluster   |
| `queue.routes`  | `QUEUE_ROUTES`  | unique channels for publishing workloads    |

{{% alert color="info" %}}
All available options support `VELA_*` prefixes for the environment variables. For example:

- `QUEUE_DRIVER` - type of client to control and operate queue
- `VELA_QUEUE_DRIVER` - type of client to control and operate queue
  {{% /alert %}}

#### Drivers

The following drivers are available to configure the component:

| Name    | Description                      | Documentation            |
| ------- | -------------------------------- | ------------------------ |
| `redis` | uses a Redis queue for workloads | https://redis.io         |
| `kafka` | uses a Kafka queue for workloads | https://kafka.apache.org |

{{% alert color="warning" %}}
Kafka is not fully supported. Using Kafka is coming soon!
{{% /alert %}}

## Limitations

These are the known limitations for this component:

#### Backups

By default, Vela **does not perform any backups of data**.

Currently, this functionality is considered out of scope for the project and should be the responsibility of the admins of the database installation.

{{% alert color="info" %}}
We recommend reviewing any available third party tools provided by the vendor to achieve this functionality.
{{% /alert %}}

#### Creation

By default, Vela **does not create your database in the system**.

Currently, this functionality is considered out of scope for the project and should be the responsibility of the admins of the database installation.

{{% alert color="info" %}}
We recommend reviewing any available third party tools provided by the vendor to achieve this functionality.
{{% /alert %}}
