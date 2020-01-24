---
title: "Go"
linkTitle: "Go"
description: >
  Learn how to write a Vela plugin with Go.
---

{{% alert color="warning" %}}
We recommend you review [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create your own plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Go documentation](https://golang.org/):

> Go is an open source programming language that makes it easy to build simple, reliable, and efficient software.

## Code

To create a plugin using Go, we'll need to first decide what task we want this plugin to accomplish. For this example, we're going to create a program that makes an HTTP request from the provided input:

```go
package main

import (
	"net/http"
	"os"
)

func main() {
	body := strings.NewReader(
		os.GetEnv("PARAMETER_BODY"),
	)

	req, err := http.NewRequest(
		os.GetEnv("PARAMETER_METHOD"),
		os.GetEnv("PARAMETER_URL"),
		body,
	)

	if err != nil {
		os.Exit(1)
	}
}
```

## Executable

Now that we have the program to accomplish our plugin's task, we need to compile the code to produce an executable binary for our target platform:

```sh
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o vela-sample
```

{{% alert color="warning" %}}
Please ensure you compile your program for the right target platform. If you don't, your plugin may fail to properly run and produce unclear error messages.
{{% /alert %}}

## Image

Once we have the executable needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image. This image should contain our binary and be setup to run that binary when the plugin is executed:

```docker
FROM alpine

RUN apk add --update --no-cache ca-certificates

COPY vela-sample /bin/vela-sample

ENTRYPOINT /bin/vela-sample
```

## Publishing

In order to run our plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t vela-sample:go .

# publish the image
docker push vela-sample:go
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that your plugin performs the desired task, you can execute it locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Go" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  vela-sample:go
```

## Usage

After publishing your image to a Docker registry, you can then reference it in a pipeline:

```yaml
version: "1"

steps:
  - name: sample_plugin
    image: vela-sample:go
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Go
```
