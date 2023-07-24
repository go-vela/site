---
no_list: true
title: "Reference"
linkTitle: "Reference"
weight: 4
description: >
  This section contains a reference of configuration options for the Vela server service.
---

## Components

The server is made up of several components, responsible for specific tasks, necessary for the service to operate:

| Name       | Description                                                                                                         |
| ---------- | ------------------------------------------------------------------------------------------------------------------- |
| `compiler` | transforms a [pipeline](/docs/tour/) into an executable workload for the [worker](/docs/installation/worker/)     |
| `database` | integrates with a database provider for storing application data at rest                                            |
| `queue`    | integrates with a queue provider for pushing workloads that will be run by a [worker](/docs/installation/worker/) |
| `secret`   | integrates with a secret provider for storing sensitive application data at rest                                    |
| `source`   | integrates with a source control management (SCM) provider for authentication and authorization                     |

## Required

This section contains a list of all variables that must be provided to the server.

### VELA_ADDR

This variable sets a fully qualified URL to the Vela [server](/docs/installation/server/) address.

The variable should be provided as a `string`.

### VELA_DATABASE_ENCRYPTION_KEY

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets the AES key for encrypting/decrypting values for data stored in the database.

The variable should be provided as an `string`.

### VELA_QUEUE_ADDR

This configuration variable is used by the [queue component](/docs/installation/server/reference/queue/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets a fully qualified URL to the queue instance for pushing workloads that will be run by a [worker](/docs/installation/worker/).

The variable should be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable should match [the `VELA_QUEUE_ADDR` variable](/docs/installation/worker/reference/#vela_queue_addr) provided to the worker.
{{% /alert %}}

### VELA_QUEUE_DRIVER

This configuration variable is used by the [queue component](/docs/installation/server/reference/queue/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets the driver to use for the queue functionality for the server.

The variable should be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable should match [the `VELA_QUEUE_DRIVER` variable](/docs/installation/worker/reference/#vela_queue_driver) provided to the worker.

The possible options to provide for this variable are:

* `redis`
{{% /alert %}}

### VELA_SCM_CLIENT

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets the client ID from the OAuth application created on the SCM system.

The variable should be provided as a `string`.

### VELA_SCM_SECRET

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets the client secret from the OAuth application created on the SCM system.

The variable should be provided as a `string`.

### VELA_SERVER_PRIVATE_KEY

This variable sets the private key that will be used to sign all JWT tokens within Vela. Please be sure to follow [guidelines](https://www.rfc-editor.org/rfc/rfc2104#section-3) related to generating a private key.

The variable should be provided as a `string`.

## Optional

This section contains a list of all variables that can be provided to the server.

### VELA_SECRET

This variable sets a shared secret with the Vela [worker](/docs/installation/worker/) for authenticating communication between workers and the server.

Only necessary to provide if utilizing the [server-worker trusted symmetric worker authentication method](/docs/installation/worker/docker/#worker-server-trusted-symmetric-token).

The variable should be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable should match [the `VELA_SERVER_SECRET` variable](/docs/installation/worker/reference/#vela_server_secret) provided to the worker.
{{% /alert %}}

### VELA_CLONE_IMAGE

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler) for the server.

The clone image sets the clone image to use for the Vela injected clone step in a pipeline.

By default, Vela will use the latest available release of the clone image at the time of a server release.

This variable should be provided as a `string`.

### VELA_COMPILER_GITHUB

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable enables using GitHub or GitHub Enterprise Server as a registry for fetching pipeline [templates](/docs/tour/templates/) from.

By default, Vela will use [GitHub](https://github.com/) as a registry for fetching templates.

However, to fetch templates from a private organization or repository on GitHub, you need to provide this configuration.

The variable can be provided as a `boolean`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `false`.
{{% /alert %}}

### VELA_COMPILER_GITHUB_TOKEN

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets a [Personal Access Token (PAT)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) for fetching pipeline [templates](/docs/tour/templates/) from GitHub or GitHub Enterprise Server.

By default, Vela will use [GitHub](https://github.com/) as a registry for fetching templates.

However, to fetch templates from a private organization or repository on GitHub, you need to provide this configuration.

The variable can be provided as a `string`.

### VELA_COMPILER_GITHUB_URL

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets a fully qualified URL to GitHub or GitHub Enterprise Server used for fetching pipeline [templates](/docs/tour/templates/) from.

By default, Vela will use [GitHub](https://github.com/) as a registry for fetching templates.

However, to fetch templates from a private organization or repository on GitHub, you need to provide this configuration.

The variable can be provided as a `string`.

### VELA_DATABASE_ADDR

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets a fully qualified URL to the database instance for storing data at rest.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `vela.sqlite`.
{{% /alert %}}

### VELA_DATABASE_COMPRESSION_LEVEL

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

This variable sets the level of compression for workload logs, uploaded by the Vela [worker](/docs/installation/worker/), which are stored in the database.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `3`.

The possible options to provide for this variable are:

* `-1`
* `0` - produces no compression for the log data
* `1` - produces compression for the log data the fastest and with the largest size of data
* `2`
* `3`
* `4`
* `5` - produces compression for the log data with an even balance of speed and size of data
* `6`
* `7`
* `8`
* `9` - produces compression for the log data the slowest and with the smallest size of data
{{% /alert %}}

### VELA_DATABASE_CONNECTION_IDLE

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

This variable sets the maximum number of [idle connections](https://pkg.go.dev/database/sql#DB.SetMaxIdleConns) allowed for the database client.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `2`.
{{% /alert %}}

### VELA_DATABASE_CONNECTION_LIFE

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

This variable sets the maximum duration of time [a connection is reusable](https://pkg.go.dev/database/sql#DB.SetConnMaxLifetime) for the database client.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `30m`.
{{% /alert %}}

### VELA_DATABASE_CONNECTION_OPEN

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

This variable sets the maximum number of [open connections](https://pkg.go.dev/database/sql#DB.SetMaxOpenConns) allowed for the database client.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `0` (meaning no limit is set).
{{% /alert %}}

### VELA_DATABASE_DRIVER

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets the driver to use for the database functionality for the server.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `sqlite3`.

The possible options to provide for this variable are:

* `postgres`
* `sqlite3`
{{% /alert %}}

### VELA_DATABASE_SKIP_CREATION

This configuration variable is used by the [database component](/docs/installation/server/reference/database/) for the server.

This variable enables skipping the creation of tables and indexes in the database system.

The variable can be provided as a `boolean`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `false`.
{{% /alert %}}

### VELA_DEFAULT_BUILD_LIMIT

This variable sets the default amount of concurrent builds a repo is allowed to run.

In this context, concurrent builds refers to any `pending` or `running` builds for that repo.

If the amount of concurrent builds for a repo matches the limit, then any new builds will be blocked from being created.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `10`.
{{% /alert %}}

### VELA_DEFAULT_BUILD_TIMEOUT

This variable sets the default duration of time a build is allowed to run on a worker.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `30`.
{{% /alert %}}

### VELA_DEFAULT_REPO_EVENTS

This variable sets the default active events for newly activated repositories.

The variable can be provided as a comma-separated `list` (i.e. `push,tag,deployment`).

{{% alert title="Note:" color="primary" %}}
By default, the `push` event is enabled. Valid values are: `push`, `pull_request`, `tag`, `deployment`, and `comment`.
{{% /alert %}}

### VELA_DISABLE_WEBHOOK_VALIDATION

This variable disables validation of webhooks sent by the SCM to the server.

The variable can be provided as a `boolean`.

{{% alert title="Note:" color="primary" %}}
This variable should only be used for local development.

This variable has a default value of `false`.
{{% /alert %}}

### VELA_ENABLE_SECURE_COOKIE

This enables using cookies with the secure flag set by the server.

The variable can be provided as a `boolean`.

{{% alert title="Note:" color="primary" %}}
This variable should only be used for local development.

This variable has a default value of `true`.
{{% /alert %}}

### VELA_MAX_BUILD_LIMIT

This variable sets the maximum amount of concurrent builds a repo is allowed to run.

In this context, concurrent builds refers to any `pending` or `running` builds for that repo.

If the amount of concurrent builds for a repo matches the limit, then any new builds will be blocked from being created.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `30`.

This variable should match [the `VELA_MAX_BUILD_LIMIT` variable](/docs/installation/ui/reference/#vela_max_build_limit) provided to the UI.
{{% /alert %}}

### VELA_MODIFICATION_ADDR

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

This variable sets a fully qualified URL to the modification endpoint used for the compiler.

The variable can be provided as a `string`.

### VELA_MODIFICATION_RETRIES

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

This variable sets the maximum number of times to resend failed requests to the modification endpoint for the compiler.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `5`.
{{% /alert %}}

### VELA_MODIFICATION_SECRET

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

This variable sets a shared secret for authenticating communication between the compiler and the modification endpoint.

The variable can be provided as a `string`.

### VELA_MODIFICATION_TIMEOUT

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler/) for the server.

This variable sets the maximum duration of time the compiler will wait before timing out requests sent to the modification endpoint.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `8s`.
{{% /alert %}}

### VELA_MAX_TEMPLATE_DEPTH

This configuration variable is used by the [compiler component](/docs/installation/server/reference/compiler) for the server.

This variable sets the maximum depth of nested templates that can be called during compilation.

The variable can be provided as an `integer`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `3`.
{{% /alert %}}

### VELA_PORT

This variable sets the port the server API responds on for HTTP requests.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `8080`.
{{% /alert %}}

### VELA_QUEUE_CLUSTER

This configuration variable is used by the [queue component](/docs/installation/server/reference/queue/) for the server.

This variable enables the server to connect to a queue cluster rather than a standalone instance.

The variable can be provided as a `boolean`.

{{% alert title="Note:" color="primary" %}}
This variable should match [the `VELA_QUEUE_CLUSTER` variable](/docs/installation/worker/reference/#vela_queue_cluster) provided to the worker.
{{% /alert %}}

### VELA_QUEUE_POP_TIMEOUT

This configuration variable is unused by the [queue component](/docs/installation/server/reference/queue/) for the server.

This variable sets the maximum duration of time the worker will wait before timing out requests sent for pushing workloads.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `60s`.
{{% /alert %}}

### VELA_QUEUE_ROUTES

This configuration variable is used by the [queue component](/docs/installation/server/reference/queue/) for the server.

This variable sets the unique channels or topics to push workloads to.

The variable can be provided as a comma-separated `list` (i.e. `myRoute1,myRoute2`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `vela`.
{{% /alert %}}

### VELA_REPO_ALLOWLIST

This variable sets a group of repositories, from the SCM, that can be enabled on the server.

The variable can be provided as a comma-separated `list` (i.e. `myOrg1/myRepo1,myOrg1/myRepo2,myOrg2/*`).

{{% alert title="Note:" color="primary" %}}
By default, no repositories are allowed to be enabled. To allow any repository to be enabled, provide a single value of `*`.
{{% /alert %}}

### VELA_SCHEDULE_ALLOWLIST

This variable sets a group of repositories, from the SCM, that can create a schedule for a repo on the server.

The variable can be provided as a comma-separated `list` (i.e. `myOrg1/myRepo1,myOrg1/myRepo2,myOrg2/*`).

{{% alert title="Note:" color="primary" %}}
By default, no repositories are allowed to create a schedule. To allow any repository to create a schedule, provide a single value of `*`.
{{% /alert %}}

### VELA_SCHEDULE_MINIMUM_FREQUENCY

This variable sets the minimum frequency allowed to be set for a schedule.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `1h`.
{{% /alert %}}

### VELA_SCM_ADDR

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets a fully qualified URL to the source control management (SCM) system.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `https://github.com`.
{{% /alert %}}

### VELA_SCM_CONTEXT

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets the message to set in the commit status on the SCM system.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `continuous-integration/vela`.
{{% /alert %}}

### VELA_SCM_DRIVER

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets the driver to use for the SCM functionality for the server.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `github`.

The possible options to provide for this variable are:

* `github`
{{% /alert %}}

### VELA_SCM_SCOPES

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets the permission scopes to apply for OAuth credentials captured from the SCM system.

The variable can be provided as a comma-separated `list` (i.e. `myScope1,myScope2`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `read:org,read:user,repo,repo:status,user:email`.
{{% /alert %}}

### VELA_SCM_WEBHOOK_ADDR

This configuration variable is used by the [SCM component](/docs/installation/server/reference/scm/) for the server.

This variable sets a fully qualified URL on the SCM system to send webhooks to the server.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of [the `VELA_ADDR` variable](/docs/installation/server/reference/#vela_addr) provided to the server.
{{% /alert %}}

### VELA_SECRET_VAULT

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable enables using HashiCorp Vault as a secret engine.

The variable can be provided as a `boolean`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `false`.
{{% /alert %}}

### VELA_SECRET_VAULT_ADDR

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets a fully qualified URL to the HashiCorp Vault instance.

The variable can be provided as a `string`.

### VELA_SECRET_VAULT_AUTH_METHOD

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

This variable sets the authentication method to obtain a token from the HashiCorp Vault instance.

The variable can be provided as a `string`.

### VELA_SECRET_VAULT_AWS_ROLE

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

This variable sets the HashiCorp Vault role to connect to the `auth/aws/login` endpoint.

The variable can be provided as a `string`.

### VELA_SECRET_VAULT_PREFIX

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

This variable sets the prefix for k/v secrets in the HashiCorp Vault instance.

The variable can be provided as a `string`.

### VELA_SECRET_VAULT_RENEWAL

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

This variable sets the frequency to renew the token for the HashiCorp Vault instance.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `30m`.
{{% /alert %}}

### VELA_SECRET_VAULT_TOKEN

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

Examples using this configuration variable are provided in the above reference documentation.

This variable sets the token for accessing the HashiCorp Vault instance.

The variable can be provided as a `string`.

### VELA_SECRET_VAULT_VERSION

This configuration variable is used by the [secret component](/docs/installation/server/reference/secret/) for the server.

This variable sets the version for the k/v backend for the HashiCorp Vault instance.

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `2`.
{{% /alert %}}

### VELA_USER_ACCESS_TOKEN_DURATION

This variable sets the maximum duration of time a Vela access token for a user is valid on the server.

The access token is used for authenticating user's requests to the server.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `15m`.
{{% /alert %}}

### VELA_USER_REFRESH_TOKEN_DURATION

This variable sets the maximum duration of time a Vela refresh token for a user is valid on the server.

The refresh token is used for refreshing a user's access token on the server.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `8h`.
{{% /alert %}}

### VELA_BUILD_TOKEN_BUFFER_DURATION

This variable sets the maximum duration of time a Vela build token for a build extends beyond the repo build limit to maintain validity on the server.

The build token is used for authenticating a worker's access to the server to update build resources.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `5m`.
{{% /alert %}}

### VELA_WEBUI_ADDR

This variable sets a fully qualified URL to the Vela [UI](/docs/installation/ui/) address.

The variable can be provided as a `string`.

### VELA_WEBUI_OAUTH_CALLBACK_PATH

This variable sets the endpoint to use for the OAuth callback path for the Vela [UI](/docs/installation/ui/).

The variable can be provided as a `string`.

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `/account/authenticate`.
{{% /alert %}}

### VELA_WORKER_AUTH_TOKEN_DURATION

This variable sets the maximum duration of time a Vela auth token for a worker is valid on the server.

The worker auth token is used for authenticating a worker's access to the server to check-in and request build tokens.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Notes:" color="primary" %}}
This variable should be _longer_ than the [VELA_CHECK_IN](/docs/installation/worker/reference/#vela_check_in) in order to be able to refresh the auth token.

This variable has a default value of `20m`.
{{% /alert %}}

### VELA_WORKER_REGISTER_TOKEN_DURATION

This variable sets the maximum duration of time a Vela registration token for a worker is valid on the server.

The worker register token is used for onboarding a worker onto the server and beginning its auth refresh routine.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Notes:" color="primary" %}}
This variable should be relatively short-lived. There is a [CLI Command](/docs/reference/cli/worker/add) to quicken the registration process for admins.

This variable has a default value of `1m`.
{{% /alert %}}

### VELA_WORKER_ACTIVE_INTERVAL

This variable sets the interval of time the workers will be considered active. A worker is considered active if it has registered with the server inside the give duration.

The variable can be provided as a `duration` (i.e. `5s`, `10m`).

{{% alert title="Note:" color="primary" %}}
This variable has a default value of `5m`.\
\
The value should coordinate with the [`VELA_CHECK_IN`](/docs/installation/worker/reference/#vela_check_in) setting provided to the [worker](/docs/installation/worker/).
{{% /alert %}}