---
title: "Bash"
linkTitle: "Bash"
description: >
  Learn how to write a Vela plugin with Bash.
---

{{% alert color="warning" %}}
We recommend you review [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create your own plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Bash documentation](https://www.gnu.org/software/bash/):

> Bash is the GNU Project's shell. Bash is the Bourne Again SHell. Bash is an sh-compatible shell that incorporates useful features from the Korn shell (ksh) and C shell (csh).
>
> It is intended to conform to the IEEE POSIX P1003.2/ISO 9945.2 Shell and Tools standard. It offers functional improvements over sh for both programming and interactive use. In addition, most sh scripts can be run by Bash without modification.

## Code

To create a plugin using Bash, we'll need to first decide what task we want this plugin to accomplish. For this example, we're going to create a script that runs a `curl` command from the provided input:

```sh
#!/bin/sh

curl \
  -X "${PARAMETER_METHOD}" \
  -d "${PARAMETER_BODY}" \
  "${PARAMETER_URL}"
```

## Executable

Now that we have the script to accomplish our plugin's task, we need to ensure the code is executable for our plugin:

```sh
chmod +x script.sh
```

## Image

Once we have the executable needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image. This image should contain our script and be setup to run that script when the plugin is executed:

```docker
FROM alpine

RUN apk add --update --no-cache ca-certificates curl

COPY script.sh /bin/script.sh

RUN chmod +x /bin/script.sh

ENTRYPOINT /bin/script.sh
```

## Publishing

In order to run our plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t vela-sample:bash .

# publish the image
docker push vela-sample:bash
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that your plugin performs the desired task, you can execute it locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Bash" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  vela-sample:bash
```

## Usage

After publishing your image to a Docker registry, you can then reference it in a pipeline:

```yaml
version: "1"

steps:
  - name: sample_plugin
    image: vela-sample:bash
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Bash
```
