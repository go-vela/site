---
title: "Services"
linkTitle: "Services"
weight: 5
description: >
  YAML tags for services block
---

The services tag is intended to be used to run applications alongside the pipeline.

```yaml
---
# This document is displaying all the required tags
# to run a postgres database for the duration of a pipeline.
services: 
  - name: postgres
    image: postgres:latest
```

## Tags

| Tag           | Required | Type            | Description                                                     |
|---------------|----------|-----------------|-----------------------------------------------------------------|
| `name`        | Y        | string          | Unique identifier for the container in the pipeline             |
| `image`       | Y        | []string        | Docker image used to create an ephemeral container                 |
| `pull`        | N        | string          | Declaration to configure if and when the Docker image is pulled |
| `environment` | N        | map || []string | Variables to inject into the container environment              |
| `entrypoint`  | N        | []string        | Commands to execute inside the container                        |
| `ports`       | N        | string          | List of ports to map for the container in the pipeline          |

### Usage

#### The `name:` tag

```yaml
---
services: 
    # Unique identifier for the container in the pipeline.
  - name: postgres
```

#### The `image:` tag

```yaml
---
services: 
    # Docker image used to create ephemeral container.
  - image: postgres:latest
```

#### The `pull:` tag

```yaml
---
services: 
    # Declaration to configure if and when the Docker image is pulled.
    # By default, the compiler will inject pull but accepts the 
    # following values: always, never, no_present, on_start, 
  - pull: always
```

#### The `environment:` tag

```yaml
---
services: 
    # Variables to injected into the container environment
    # using a map style syntax.
  - environment:
      DB_NAME: vela
```

```yaml
---
services: 
    # Variables to injected into the container environment
    # using an array style syntax.
  - environment:
      - DB_NAME=vela
```

#### The `entrypoint:` tag

```yaml
---
services: 
    # Commands to execute inside the container.
  - entrypoint:
      - some/path/sql-init.sql
      - /some/binary/postgres
```

#### The `ports:` tag

```yaml
---
services: 
    # List of ports to map for the container in the pipeline.
  - ports: 
      - "8080:5432"
```
