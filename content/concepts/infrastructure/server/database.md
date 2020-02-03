---
title: "Database"
linkTitle: "Database"
description: >
  This section contains information on the database server component.
---

The `database` component is one of the server components for Vela.

This component defines the system Vela uses for storing its [data at rest](https://en.wikipedia.org/wiki/Data_at_rest). This data is an organized collection of information necessary for the platform to operate.

## Configuration

The following options are used to configure the component:

| Name                       | Environment                | Description                                    |
| -------------------------- | -------------------------- | ---------------------------------------------- |
| `database.driver`          | `DATABASE_DRIVER`          | type of client to control and operate database |
| `database.config`          | `DATABASE_CONFIG`          | full connection string to database             |
| `database.connection.open` | `DATABASE_CONNECTION_OPEN` | total number of open connections to database   |
| `database.connection.idle` | `DATABASE_CONNECTION_IDLE` | total number of idle connections to database   |
| `database.connection.life` | `DATABASE_CONNECTION_LIFE` | total amount of time a connection is reusable  |

{{% alert color="info" %}}
All available options support `VELA_*` prefixes for the environment variables. For example:
* `DATABASE_DRIVER` - type of client to control and operate database
* `VELA_DATABASE_DRIVER` - type of client to control and operate database
{{% /alert %}}

#### Drivers

The following drivers are available to configure the component:

| Name       | Description                            | Documentation              |
| ---------- | -------------------------------------- | -------------------------- |
| `sqlite3`  | uses a SQLite database for storage     | https://www.sqlite.org     |
| `postgres` | uses a PostgreSQL database for storage | https://www.postgresql.org |

## Limitations

These are the known limitations for this component:

#### Archives

By default, Vela **does not perform any archival of data**.

Currently, this functionality is considered out of scope for the project and should be the responsibility of the admins of the database installation.

{{% alert color="info" %}}
We recommend reviewing any available third party tools provided by the vendor to achieve this functionality.
{{% /alert %}}

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

#### Migration

By default, Vela **does not handle data migrations**.

Currently, this functionality is considered out of scope for the project and should be the responsibility of the admins of the database installation.

{{% alert color="info" %}}
We recommend reviewing any available third party tools provided by the vendor to achieve this functionality.
{{% /alert %}}
