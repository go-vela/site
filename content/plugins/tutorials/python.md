---
title: "Python"
linkTitle: "Python"
description: >
  Learn how to write a Vela plugin with Python.
---

{{% alert color="warning" %}}
We recommend reviewing [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create a custom plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Python documentation](https://www.python.org/):

> Python is a programming language that lets you work quickly and integrate systems more effectively.

## Code

To create a plugin using Python, we'll need to first decide what task we want this plugin to accomplish.

For this example, we're going to create a program that makes an HTTP request from the provided input:

```python
#!/usr/bin/env python

import http.client
import os
import urlparse

# import method parameter from environment
method = os.getenv['PARAMETER_METHOD']
# import body parameter from environment
body = os.getenv['PARAMETER_BODY']
# import url parameter from environment
url = os.getenv['PARAMETER_URL']

# capture full URI from url
uri = urlparse(url)

# create new HTTP connection from URL
conn = http.client.HTTPSConnection(uri.hostname, uri.port)

# create headers to be added to request
headers = {}

# send HTTP request
conn.request(method, uri.path, body, headers)

# capture the response
response = conn.getresponse()

# output the response
print(response.read().decode("utf-8"))
```

{{% alert color="info" %}}
An example of this code is provided in the [python section](https://github.com/go-vela/vela-tutorials/tree/master/plugins/python) of the [go-vela/vela-tutorials](https://github.com/go-vela/vela-tutorials/tree/master/plugins) repository.
{{% /alert %}}

## Image

Once we have the script needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image.

This image should contain the script and be setup to run that script when the plugin is executed:

```docker
FROM python:alpine

RUN apk add --update --no-cache ca-certificates

COPY vela-sample.py /bin/vela-sample.py

ENTRYPOINT ["python", "/bin/vela-sample.py"]
```

{{% alert color="info" %}}
An example of this image is provided in the [target/vela-sample](https://hub.docker.com/r/target/vela-sample) Docker repository.
{{% /alert %}}

## Publishing

In order to run the plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t target/vela-sample:python .

# publish the image
docker push target/vela-sample:python
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that the plugin performs the desired task, it can be executed locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Python" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  target/vela-sample:python
```

## Usage

After publishing the image to a Docker registry, it can be referenced in a pipeline:

```yaml
version: "1"

steps:
  - name: sample python plugin
    image: target/vela-sample:python
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Python
```
