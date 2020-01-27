---
title: "Python"
linkTitle: "Python"
description: >
  Learn how to write a Vela plugin with Python.
---

{{% alert color="warning" %}}
We recommend you review [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create your own plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Python documentation](https://www.python.org/):

> Python is a programming language that lets you work quickly and integrate systems more effectively.

## Code

To create a plugin using Python, we'll need to first decide what task we want this plugin to accomplish. For this example, we're going to create a program that makes an HTTP request from the provided input:

```python
#!/usr/bin/env python

import requests

response = requests.request(
    os.environ['PARAMETER_METHOD'],
    os.environ['PARAMETER_URL'],
    data = os.environ['PARAMETER_BODY']
)

print(response.text.encode('utf8'))
```

## Executable

Now that we have the script to accomplish our plugin's task, we need to ensure the code is executable for our plugin:

```sh
chmod +x script.py
```

## Image

Once we have the executable needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image. This image should contain our script and be setup to run that script when the plugin is executed:

```docker
FROM alpine

RUN apk add --update --no-cache ca-certificates python

COPY script.py /bin/script.py

ENTRYPOINT ["python", "/bin/script.py"]
```

## Publishing

In order to run our plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t vela-sample:python .

# publish the image
docker push vela-sample:python
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that your plugin performs the desired task, you can execute it locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Python" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  vela-sample:python
```

## Usage

After publishing your image to a Docker registry, you can then reference it in a pipeline:

```yaml
version: "1"

steps:
  - name: sample_plugin
    image: vela-sample:python
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Python
```
