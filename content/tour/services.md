---
title: "Services"
linkTitle: "Services"
weight: 7
description: >
  Learn about services.
---

This declaration allows you to provide detached (headless) container for the duration of a pipeline.

Services are always ran, in parallel alongside the ephemeral steps in the pipeline. They are extremely useful when your testing requires additional services such as a cache, database or queue.

Services are always created at the beginning of a pipeline in the order they are defined.

The `name:` field of the service defines at what hostname the service will be available.

However, there are times when you need more control over when a service is created. Perhaps you are dealing with a service that has start up dependencies and service A needs some to to start up before service B is started

<!-- section break -->

```yaml
services:
  # Starting a set of services at the beginning of 
  # pipeline execution
  - name: cache
    image: redis
  - name: database
    image: mongo
```

```yaml
version: "1"
services:
  # Starting a set of services at the beginning of 
  # pipeline execution
  - name: cache
    image: redis

steps:
  - name: ping cache
    image: redis
    commands:
      - redis-cli -h cache ping

  # Now that we know redis is started we execute another 
  # service directly in the steps workflow
  - name: database
    image: postgres
    detach: true
```

```sh
$ vela exec pipeline

[service: cache] 1:C 02 Feb 2021 21:24:10.600 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
[service: cache] 1:C 02 Feb 2021 21:24:10.600 # Redis version=6.0.10, bits=64, commit=00000000, modified=0, pid=1, just started
[service: cache] 1:C 02 Feb 2021 21:24:10.600 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
[service: cache] 1:M 02 Feb 2021 21:24:10.602 * Running mode=standalone, port=6379.
[service: cache] 1:M 02 Feb 2021 21:24:10.603 # WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.
[service: cache] 1:M 02 Feb 2021 21:24:10.603 # Server initialized
[service: cache] 1:M 02 Feb 2021 21:24:10.603 * Ready to accept connections
[stage: ][step: ping cache] $ redis-cli -h cache ping
[stage: ][step: ping cache] PONG
```

<!-- section break -->

**Tag references:**

[`name:`](/docs/reference/yaml/services/#the-name-tag), [`image:`](/docs/reference/yaml/services/#the-image-tag), [`detach:`](/docs/reference/yaml/steps/#the-detach-tag), 