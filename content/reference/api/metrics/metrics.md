---
title: "Metrics"
linkTitle: "Metrics"
description: >
  Learn how to list metrics.
---

## Endpoint

```
GET  /metrics
```

## Query Parameters

The following parameters are used to configure the endpoint:

| Query Parameter         | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| `user_count`            | count of total users                                    |
| `repo_count`            | count of total repos                                    |
| `build_count`           | count of total builds                                   |
| `running_build_count`   | count of builds with status 'running'                   |
| `failure_build_count`   | count of builds with status 'failure'                   |
| `pending_build_count`   | count of builds with status 'pending'                   |
| `queued_build_count`    | count of builds inside the queue                        |
| `killed_build_count`    | count of builds with status 'killed'                    |
| `success_build_count`   | count of builds with status 'success'                   |
| `error_build_count`     | count of builds with status 'error'                     |
| `step_image_count`      | count of total steps executed with each unique image    |
| `step_status_count`     | count of total steps with each status                   |
| `service_image_count`   | count of total services executed with each unique image |
| `service_status_count`  | count of total services with each status                |
| `worker_build_limit`    | count of worker build limits                            |
| `active_worker_count`   | count of active workers                                 |
| `inactive_worker_count` | count of inactive workers                               |


## Permissions

No permission restrictions for this endpoint.

## Responses

| Status Code | Description                                             |
| ----------- | ------------------------------------------------------- |
| `200`       | indicates the request has succeeded                     |
| `500`       | indicates a server failure while processing the request |

## Sample

#### Request

```sh
curl \
  -X GET \
  "http://127.0.0.1:8080/metrics?pending_build_count=true"
```

#### Response

```json
# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 4.0986e-05
# TYPE vela_totals gauge
vela_totals{field="status",resource="build",value="pending"} 31
```
