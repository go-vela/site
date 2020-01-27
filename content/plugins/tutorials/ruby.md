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

# import method parameter from environment
method = ENV['PARAMETER_METHOD']
# import body parameter from environment
body = ENV['PARAMETER_BODY']
# import url parameter from environment
url = ENV['PARAMETER_URL']

# check if a method parameter was provided
if method.empty?
  puts "no method parameter provided"
  exit(1)
end

# check if a body parameter was provided
if body.empty?
  puts "no body parameter provided"
  exit(1)
end

# check if a url parameter was provided
if url.empty?
  puts "no url parameter provided"
  exit(1)
end

# capture full URI from url
uri = URI(url)

# create new HTTP client from URI
http = Net::HTTP.new(uri.host, uri.port)

# send HTTP request and capture response
response = http.send_request(
  method,
  uri.path,
  body,
)

# output the response
puts response.read_body
```

## Image

Once we have the script needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image. This image should contain our script and be setup to run that script when the plugin is executed:

```docker
FROM ruby:alpine

RUN apk add --update --no-cache ca-certificates

COPY vela-sample.rb /bin/vela-sample.rb

ENTRYPOINT ["ruby", "/bin/vela-sample.rb"]
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
