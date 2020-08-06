---
title: "Node.js"
linkTitle: "Node.js"
description: >
  Learn how to write a Vela plugin with Node.js.
---

{{% alert color="warning" %}}
We recommend reviewing [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create a custom plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Node.js documentation](https://nodejs.org/):

> As an asynchronous event-driven JavaScript runtime, Node.js is designed to build scalable network applications.

## Code

To create a plugin using Node.js, we'll need to first decide what task we want this plugin to accomplish.

For this example, we're going to create a program that makes an HTTP request from the provided input:

```javascript
#!/usr/bin/env node

const https = require("https");
const url = require("url");

// import method parameter from environment
const method = process.env.PARAMETER_METHOD;
// import body parameter from environment
const body = process.env.PARAMETER_BODY;
// import url parameter from environment
const uri = process.env.PARAMETER_URL;

// capture full URL from uri
const myURL = url.parse(uri);

// create options for HTTP request
const options = {
  method: method
};

// create new HTTP request from provided input
const req = https.request(myURL, options);

// exit immediately if request errors
req.on("error", () => {
  process.exit(1);
});

// write body to HTTP request
req.write(process.env.PARAMETER_BODY);

// send HTTP request
req.end();
```

{{% alert color="info" %}}
An example of this code is provided in the [node.js section](https://github.com/go-vela/vela-tutorials/tree/master/plugins/node.js) of the [go-vela/vela-tutorials](https://github.com/go-vela/vela-tutorials/tree/master/plugins) repository.
{{% /alert %}}

## Image

Once we have the executable needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image.

This image should contain the script and be setup to run that script when the plugin is executed:

```docker
FROM node:alpine

RUN apk add --update --no-cache ca-certificates

COPY vela-sample.js /bin/vela-sample.js

ENTRYPOINT ["node", "/bin/vela-sample.js"]
```

{{% alert color="info" %}}
An example of this image is provided in the [target/vela-sample](https://hub.docker.com/r/target/vela-sample) Docker repository.
{{% /alert %}}

## Publishing

In order to run the plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t target/vela-sample:node .

# publish the image
docker push target/vela-sample:node
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that the plugin performs the desired task, it can be executed locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Node.js" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  target/vela-sample:node
```

## Usage

After publishing the image to a Docker registry, it can be referenced in a pipeline:

```yaml
version: "1"

steps:
  - name: sample node plugin
    image: target/vela-sample:node
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Node.js
```
