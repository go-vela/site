---
title: "Ruby"
linkTitle: "Ruby"
description: >
  Learn how to write a Vela plugin with Ruby.
---

{{% alert color="warning" %}}
We recommend you review [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create your own plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Ruby documentation](https://www.ruby-lang.org/en/):

> Ruby is...
>
> A dynamic, open source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.

## Code

To create a plugin using Ruby, we'll need to first decide what task we want this plugin to accomplish. For this example, we're going to create a program that makes an HTTP request from the provided input:

```ruby
#!/usr/bin/env ruby

require 'net/http'
require 'uri'

uri = URI.parse(ENV['PARAMETER_URL'])

http = Net::HTTP.new(uri.host, uri.port)

response = http.send_request(
  ENV['PARAMETER_METHOD'],
  '',
  ENV['PARAMETER_BODY'],
)

puts response
```

## Image

Once we have the script needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image. This image should contain our script and be setup to run that script when the plugin is executed:

```docker
FROM ruby:alpine

RUN apk add --update --no-cache ca-certificates

COPY script.rb /bin/script.rb

ENTRYPOINT ["ruby", "/bin/script.rb"]
```

## Publishing

In order to run our plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t vela-sample:ruby .

# publish the image
docker push vela-sample:ruby
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that your plugin performs the desired task, you can execute it locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Ruby" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  vela-sample:ruby
```

## Usage

After publishing your image to a Docker registry, you can then reference it in a pipeline:

```yaml
version: "1"

steps:
  - name: sample_plugin
    image: vela-sample:ruby
    pull: true
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Ruby
```
