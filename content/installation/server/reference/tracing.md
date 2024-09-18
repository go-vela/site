---
title: "Tracing"
linkTitle: "Tracing"
weight: 7
description: >
  This section contains information on configuring OpenTelemetry instrumentation for the Vela server.
---

This component is responsible for instrumenting [OpenTelemetry traces](https://opentelemetry.io/docs/concepts/signals/traces/) based off the configuration provided.

## Configuration

The following options are used to configure the component:

| Name                        | Description                                              | Required | Default | Environment Variables                                                       |
| --------------------------- | -------------------------------------------------------- | -------- | ------- | --------------------------------------------------------------------------- |
| `tracing.enable` | This variable enables [OpenTelemetry tracing](https://opentelemetry.io/docs/concepts/signals/traces/) for the Vela server. You must provide `VELA_OTEL_EXPORTER_OTLP_ENDPOINT` **when tracing is enabled**. | `false` | `false` | `VELA_OTEL_TRACING_ENABLE` |
| `tracing.service.name` | This variable sets the [service name](https://opentelemetry.io/docs/languages/sdk-configuration/general/) applied to [traces](https://opentelemetry.io/docs/concepts/signals/traces/). | `false` | `vela-server` | `VELA_OTEL_TRACING_SERVICE_NAME` |
| `tracing.exporter.endpoint` | This variable sets the [OTel exporter](https://opentelemetry.io/docs/languages/sdk-configuration/otlp-exporter/) endpoint (ex. scheme://host:port). | `false` | `N/A` | `VELA_OTEL_EXPORTER_OTLP_ENDPOINT` |
| `tracing.exporter.cert_path` | This variable sets the path to certs used for communicating with the [OTel exporter](https://opentelemetry.io/docs/specs/OTel/protocol/exporter/). If nothing is provided the server will use insecure communication. | `false` | `N/A` | `VELA_OTEL_TRACING_EXPORTER_SSL_CERT_PATH` |
| `tracing.exporter.tls-min-version` | This optional variable sets a TLS minimum version used when exporting traces to the [OTel exporter](https://opentelemetry.io/docs/specs/OTel/protocol/exporter/). | `false` | `1.2` | `VELA_OTEL_TRACING_TLS_MIN_VERSION` |
| `tracing.sampler.persecond` | This variable sets OTel [tracing head-sampler](https://opentelemetry.io/docs/concepts/sampling/) rate-limiting to N per second. | `false` | `100` | `VELA_OTEL_TRACING_SAMPLER_RATELIMIT_PER_SECOND` |
| `tracing.sampler.tasks` | This variable sets an (optional) filepath to the OTel tracing head-sampler configurations json to alter how certain tasks (API endpoints, queries, etc) are sampled. | `false` | `N/A` | `VELA_OTEL_TRACING_SAMPLER_TASKS_CONFIG_FILEPATH` |
| `tracing.resource.attributes` | This variable sets OTel resource [(span) attributes](https://opentelemetry.io/docs/languages/go/instrumentation/#span-attributes) as a list of `key=value` pairs. each one will be attached to each span as a 'process' attribute. | `false` | `N/A` | `VELA_OTEL_TRACING_RESOURCE_ATTRIBUTES` |
| `tracing.resource.env_attributes` | This variable sets OTel resource [(span) attributes](https://opentelemetry.io/docs/languages/go/instrumentation/#span-attributes) as a list of `key=env_variable_key` pairs. each one will be attached to each [span](https://opentelemetry.io/docs/languages/go/instrumentation/#span-attributes) as a 'process' attribute where the value is retrieved from the environment using the pair value. | `false` | `N/A` | `VELA_OTEL_TRACING_RESOURCE_ENV_ATTRIBUTES` |
| `tracing.span.attributes` | This variable sets trace [span attributes](https://opentelemetry.io/docs/languages/go/instrumentation/#span-attributes) as a list of `key=value` pairs. Each pair will be attached to each [span](https://opentelemetry.io/docs/languages/go/instrumentation/#span-attributes) as a 'tag' attribute. | `false` | `N/A` | `VELA_OTEL_TRACING_SPAN_ATTRIBUTES` |
| `tracing.tracestate.attributes` | This variable sets OTel tracestate [(span) attributes](https://www.w3.org/TR/trace-context) as a list of `key=value` pairs. Each pair will be inserted into the tracestate for each sampled span. | `false` | `N/A` | `VELA_OTEL_TRACING_TRACESTATE_ATTRIBUTES` |

{{% alert title="Note:" color="primary" %}}
For more information on how the runtime properties are consumed, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}

## Exporter

To start using tracing you first need to set `VELA_OTEL_TRACING_ENABLE=true` in the runtime environment. 

Enabling tracing requires that `VELA_OTEL_EXPORTER_OTLP_ENDPOINT` be set to an [exporter](https://opentelemetry.io/docs/specs/OTel/protocol/exporter/) host that is reachable over HTTP. 

If the exporter requires SSL then `VELA_OTEL_TRACING_EXPORTER_SSL_CERT_PATH` must be set to a filepath that contains valid certificates. If no certificate filepath is set, then the server will communicate with the exporter over HTTP (insecure).

The Vela local stack is configured to export traces to Jaeger using their "all-in-one" Docker image, making it easy to view traces out of the box.

```diff
+   jaeger:
+     image: jaegertracing/all-in-one:latest
...

$ docker run \
  --detach=true \
  --env=VELA_ADDR=https://vela-server.example.com \
+ --env=VELA_OTEL_TRACING_ENABLE: true \
+ --env=VELA_OTEL_EXPORTER_OTLP_ENDPOINT: http://jaeger:4318 \
...
```

From the [Jaeger official website](https://www.jaegertracing.io/docs/1.6/getting-started/):
> This image, designed for quick local testing, launches the Jaeger UI, collector, query, and agent, with an in memory storage component.

## Sampling

The server uses a combination of "shared" and "per-task" [head sampling](https://opentelemetry.io/docs/concepts/sampling/) to control how traces are recorded or dropped.

### "Shared" Samplers

The following samplers are utilized by all traces produced by the server.

#### Global Rate-limiting

All traces share a global rate limit controlled by `VELA_OTEL_TRACING_SAMPLER_RATELIMIT_PER_SECOND`.

Use `VELA_OTEL_TRACING_SAMPLER_RATELIMIT_PER_SECOND` to set a maximum threshold of "N traces per second". The default is `100` traces per second.

### "Task" Samplers

Set `VELA_OTEL_TRACING_SAMPLER_TASKS_CONFIG_FILEPATH` to point to a JSON filepath to control sampler configurations on a per-task basis.

```json
tracing.json
{
    "task-name": {
        "active": bool
    }
}
```

A `task` is basically the "span name" based on the work being performed. A `task` can be an API endpoint interaction, a [Gorm](https://gorm.io/docs/index.html) query, etc. See [OTel span docs](https://opentelemetry.io/docs/specs/otel/trace/api/#span) for more information.

If a `task` is **not** represented in the configuration file then the task will be treated normally, **with tracing enabled** using the "shared" samplers.

| Field | Type | Description |
| ----- | ----------- | ----------- |
| `active` | bool | Set to `false` to completely disable traces for a particular task. |

Examples of trace tasks include API endpoints, gorm queries, etc. The list of tasks will change as functionality is added to the server.

> See the configuration file examples below.

#### Example - No Tasks

```json
{}
```

Because tasks that do not exist in the configuration file will be treated as enabled, this file will **enable all tracing**.

#### Example - Disable /health Endpoint

```json
{
    "/health": {
        "active": false
    }
}
```

Because `active` can be used to disable tracing, this configuration file will enable tracing for all tasks **except for the `/health` endpoint**.

#### Example - Mixed Tasks

```json
{
    "/health": {
        "active": false
    },
    "/api/v1/deployments/:org/:repo": {
        "active": false
    },
    "/api/v1/:worker": {
        "active": true
    },
    "gorm.query": {
        "active": false
    }
}
```

The task `/health` with `active: false` will **disable** tracing on `/health`.

`/api/v1/deployments/:org/:repo` with `active: false` will **disable** tracing on `/api/v1/deployments/:org/:repo` for **ALL** `:org` and `:repo` parameters.

`/api/v1/:worker` with `active: true` **will do nothing** at this point, because any tasks that are not present in the configuration file will automatically be sampled normally. For now this is slightly confusing, but in the future there will be more configuration fields that will determine how an `active: true` task is sampled.

The task `gorm.query` with `active: false` would disable tracing for raw gorm queries. This is meant to show that the config applies to **all trace tasks** and not just API endpoints.

**All other tasks** will be sampled as normal using the global shared samplers (like rate limiting)! This includes all API endpoints and gorm queries.
