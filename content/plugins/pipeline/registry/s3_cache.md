---
title: "S3 Cache"
---

## Overview

This plugin enables you to cache build resources in an [s3](https://aws.amazon.com/s3/) compatible store for a Vela pipeline.

Source Code: https://github.com/go-vela/vela-s3-cache

Registry: https://hub.docker.com/r/target/vela-s3-cache

{{% alert color="tip" %}}
This plugin supports environment (`PARAMETER_*`) and volume (`/vela/parameters/*`) configuration for setting parameters.

The precedence order is take files then environment variables if both are set in a container.
{{% /alert %}}

## Usage

Sample of restoring a cache:

```yaml
steps:
  - name: restore_cache
    image: target/vela-s3-cache:v0.2.0
    pull: true
    parameters:
      action: restore
      root: mybucket
      server: mybucket.s3-us-west-2.amazonaws.com
```

Sample of rebuilding a cache:

```yaml
steps:
  - name: rebuild_cache
    image: target/vela-s3-cache:v0.2.0
    pull: true
    parameters:
      action: rebuild
      root: mybucket
      server: mybucket.s3-us-west-2.amazonaws.com
      mount:
        - .gradle
```

Sample of flushing a cache:

```yaml
steps:
  - name: flushing_cache
    image: target/vela-s3-cache:v0.2.0
    pull: true
    parameters:
      action: flush
      root: mybucket
      server: mybucket.s3-us-west-2.amazonaws.com
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.
{{% /alert %}}

### Internal

The plugin accepts the following `parameters` for authentication:

| Parameter       | Environment Variable Configuration                                       |
| --------------- | ------------------------------------------------------------------------ |
| `access_key`    | `AWS_ACCESS_KEY_ID`, `CACHE_S3_ACCESS_KEY`, `PARAMETER_ACCESS_KEY`       |
| `secret_key`    | `AWS_SECRET_ACCESS_KEY`, `CACHE_S3_SECRET_KEY`, `PARAMETER_SECRET_KEY`   |
| `session_token` | `AWS_SESSION_TOKEN`, `CACHE_S3_SESSION_TOKEN`, `PARAMETER_SESSION_TOKEN` |

Users can use [Vela secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: restore_cache
    image: target/vela-s3-cache:v0.2.0
    pull: true
+   secrets: [ cache_s3_access_key, cache_s3_secret_key ]
    parameters:
      action: restore
      root: mybucket
      server: mybucket.s3-us-west-2.amazonaws.com
-     access_key: AKIAIOSFODNN7EXAMPLE
-     secret_key: 123456789QWERTYEXAMPLE
```

{{% alert color="info" %}}
This example will add the `secrets` to the `restore_cache` step as environment variables:

- `CACHE_S3_ACCESS_KEY`=<value>
- `CACHE_S3_SECRET_KEY`=<value>
{{% /alert %}}

### External

The plugin accepts the following files for authentication:

| Parameter       | Volume Configuration                                                       |
| --------------- | ------------------------------------------------------------------------ |
| `access_key`    | `/vela/parameters/s3_cache/config/access_key`, `/vela/secrets/s3_cache/config/access_key`       |
| `secret_key`    | `/vela/parameters/s3_cache/config/secret_key`, `/vela/secrets/s3_cache/config/secret_key`   |
| `session_token` | `/vela/parameters/s3_cache/config/session_token`, `/vela/secrets/s3_cache/config/session_token` |

Users can use [Vela external secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: restore_cache
    image: target/vela-s3-cache:v0.2.0
    pull: true
    parameters:
      action: restore
      root: mybucket
      server: mybucket.s3-us-west-2.amazonaws.com
-     access_key: AKIAIOSFODNN7EXAMPLE
-     secret_key: 123456789QWERTYEXAMPLE
```

{{% alert color="info" %}}
This example will read the secrets values in the volume stored at `/vela/secrets/`:
{{% /alert %}}

## Parameters

The following parameters can used to configure all image actions:

| Name         | Description                          | Required | Default |
| ------------ | ------------------------------------ | -------- | ------- |
| `action`     | action to perform against s3         | `true`   | `N/A`   |
| `log_level`  | set the log level for the plugin     | `true`   | `info`  |
| `server`     | s3 instance to communicate with      | `true`   | `N/A`   |
| `access_key` | access key for communication with s3 | `true`   | `N/A`   |
| `secret_key` | secret key for communication with s3 | `true`   | `N/A`   |
| `root`       | name of the s3 bucket                | `true`   | `N/A`   |
| `prefix`     | path prefix for the object(s)        | `true`   | `N/A`   |

#### Restore

The following parameters are used to configure the `restore` action:

| Name       | Description                                                | Required | Default |
| ---------- | ---------------------------------------------------------- | -------- | ------  |
| `filename` | the name of the cache object                               | `false`  | `true`  |
| `mount`    | the file or directories locations to build your cache from | `true`   | `N/A`   |
| `timeout`  | the timeout for the call to s3                             | `false`  | `true`  |


#### Rebuild

The following parameters are used to configure the `rebuild` action:

| Name       | Description                    | Required | Default |
| ---------- | ------------------------------ | -------- | ------  |
| `filename` | the name of the cache object   | `false`  | `true`  |
| `timeout`  | the timeout for the call to s3 | `false`  | `true`  |

#### Flush

The following parameters are used to configure the `flush` action:

| Name  | Description                              | Required | Default |
| ----- | ---------------------------------------- | -------- | ------- |
| `age` | delete the objects past a specific age   | `false`  | `14`    |

#### Upload

## Template

COMING SOON!

## Troubleshooting

You can start troubleshooting this plugin by tuning the level of logs being displayed:

```diff
steps:
  - name: restore_cache
    image: target/vela-s3-cache:v0.2.0
    pull: true
    parameters:
      action: restore
+     log_level: trace
      root: mybucket
      server: mybucket.s3-us-west-2.amazonaws.com
```

Below are a list of common problems and how to solve them:

COMING SOON!
