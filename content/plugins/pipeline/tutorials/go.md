---
title: "Go"
linkTitle: "Go"
description: >
  Learn how to write a Vela plugin with Go.
---

{{% alert color="warning" %}}
We recommend reviewing [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create a custom plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Go documentation](https://golang.org/):

> Go is an open source programming language that makes it easy to build simple, reliable, and efficient software.

## Code

To create a plugin using Go, we'll need to first decide what task we want this plugin to accomplish.

For this example, we're going to create a program that makes an HTTP request from the provided input:

```go
package main

import (
	"fmt"
	"net/http"
	"os"
	"strings"
)

func main() {
	// import method parameter from environment
	method := os.Getenv("PARAMETER_METHOD")
	// import body parameter from environment
	body := os.Getenv("PARAMETER_BODY")
	// import url parameter from environment
	url := os.Getenv("PARAMETER_URL")

	// create payload from body
	payload := strings.NewReader(body)

	// create new HTTP request from provided input
	request, err := http.NewRequest(method, url, payload)
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}

	// send HTTP request and capture response
	response, err := http.DefaultClient.Do(request)
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}

	// output the response
	fmt.Println(response)
}
```

{{% alert color="info" %}}
An example of this code is provided in the [go section](https://github.com/go-vela/vela-tutorials/tree/master/plugins/go) of the [go-vela/vela-tutorials](https://github.com/go-vela/vela-tutorials/tree/master/plugins) repository.
{{% /alert %}}

## Executable

Now that we have the program to accomplish our plugin's task, we need to compile the code to produce an executable binary for the target platform:

```sh
GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o vela-sample
```

{{% alert color="warning" %}}
Please ensure the program is compiled for the right target platform.

If it's not, the plugin may fail to properly run and produce unclear error messages.
{{% /alert %}}

## Image

Once we have the executable needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image.

This image should contain the binary and be setup to run that binary when the plugin is executed:

```docker
FROM golang:alpine

RUN apk add --update --no-cache ca-certificates

COPY vela-sample /bin/vela-sample

ENTRYPOINT ["/bin/vela-sample"]
```

{{% alert color="info" %}}
An example of this image is provided in the [target/vela-sample](https://hub.docker.com/r/target/vela-sample) Docker repository.
{{% /alert %}}

## Publishing

In order to run the plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t target/vela-sample:go .

# publish the image
docker push target/vela-sample:go
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that the plugin performs the desired task, it can be executed locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Go" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  target/vela-sample:go
```

## Usage

After publishing the image to a Docker registry, it can be referenced in a pipeline:

```yaml
version: "1"

steps:
  - name: sample go plugin
    image: target/vela-sample:go
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Go
```
