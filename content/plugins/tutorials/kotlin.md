---
title: "Kotlin"
linkTitle: "Kotlin"
description: >
  Learn how to write a Vela plugin with Kotlin.
---

{{% alert color="warning" %}}
We recommend reviewing [Docker's best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) before attempting to create a custom plugin.

We recommend that all plugins be placed inside a [scratch image](https://hub.docker.com/_/scratch).
{{% /alert %}}

## Overview

From [Kotlin documentation](https://www.kotlinlang.org/):

> Kotlin is...
>
> A modern, concise and safe programming language that is easy to pick up, so you can create powerful applications immediately

## Code

To create a plugin using Kotlin, we'll need to first decide what task we want this plugin to accomplish.

For this example, we're going to create a program that makes an HTTP request from the provided input:

```kotlinlang
import org.http4k.client.ApacheClient
import org.http4k.core.*
import org.http4k.format.Jackson.auto
import yellowstone.cr.VCRException

fun main() {
    // get the vela parameters from env variables
    val method = when ("METHOD".parameter.envOrDefault("GET").trim().lowercase()) {
        "get" -> Method.GET
        "put" -> Method.PUT
        "post" -> Method.POST
        "delete" -> Method.DELETE
        else -> throw Exception("Method not supported")
    }
    val body = "BODY".parameter.env
    val url = "URL".parameter.env

    // set up the clientId
    val client: HttpHandler = ApacheClient()

    // make the request and print the result
    println(Request(method, url).addBody(body).okOrDie(client).toObject<String>())
}

// Helper functions
val String.env get() = System.getenv(this) ?: throw VCRException("The environment variable $this is required but missing!")
fun String.envOrDefault(default: String) = System.getenv(this) ?: default
val String.parameter get() = "PARAMETER_$this"
fun Request.okOrDie(client: HttpHandler) = client(this).let { response ->
    response.takeIf { it.status.successful }
        ?: throw Exception("Got unexpected ${response.status.code} from request ${method.name} $uri! ${response.bodyString()}")
}

inline fun <reified T : Any> Response.toObject() = Body.auto<T>().toLens()(this)
inline fun <reified T : Any> Request.addBody(t: T) = Body.auto<T>().toLens()(t, this)
```

## Jar

In order to make this code a runnable executable, you must first turn it into a jar file.  Below is an example `build.gradle.kts`

```kotlinlang
import org.jetbrains.kotlin.gradle.tasks.KotlinCompile

plugins {
    application
    kotlin("jvm") version "1.5.10"
}

repositories {
    mavenCentral()
}

application {
    group = "mygroup"
    mainClass.set("mygroup.MainKt")
}

dependencies {
    fun deps(format: String, vararg arr: String) = with(format) { arr.forEach { implementation(format(it)) } }

    implementation(kotlin("stdlib-jdk8"))
    implementation(kotlin("reflect"))
    deps("org.http4k:http4k-%s:4.9.9.0", "client-apache", "format-jackson")
}

tasks {
    jar {
        enabled = true
    }
    withType<KotlinCompile> {
        kotlinOptions.jvmTarget = JavaVersion.VERSION_11.majorVersion
    }
    withType<Test> {
        useJUnitPlatform()
    }
}
```

To build the jar, run `./gradlew clean build distTar`

## Image

Once we have the jar needed to accomplish our plugin's task, we need to create a Dockerfile to produce an image.

This image should contain the jar and be setup to run that jar when the plugin is executed

```docker
FROM alpine:latest

# Install Java 11
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-11-openjdk/jre/bin:/usr/lib/jvm/java-11-openjdk

RUN apk update && \
    apk upgrade && \
    apk --no-cache add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community

# copy the executable
ADD build/distributions/vela-sample.tar /

CMD ["/vela-sample/bin/vela-sample"]
```

## Publishing

In order to run the plugin in a pipeline, we'll need to make sure we build and publish it to a Docker registry:

```sh
# build the image
docker build -t target/vela-sample:kotlin .

# publish the image
docker push target/vela-sample:kotlin
```

{{% alert color="info" %}}
This has the added benefit of enabling others in the community to consume your plugin!
{{% /alert %}}

## Troubleshooting

To verify that the plugin performs the desired task, it can be executed locally via the command line:

```sh
docker run --rm \
  -e PARAMETER_BODY="This is a sample Vela plugin written with Kotlin" \
  -e PARAMETER_METHOD="POST" \
  -e PARAMETER_URL="http://vela.localhost.com" \
  target/vela-sample:kotlin
```

## Usage

After publishing the image to a Docker registry, it can be referenced in a pipeline:

```yaml
version: "1"

steps:
  - name: sample kotlin plugin
    image: target/vela-sample:kotlin
    pull: always
    parameters:
      url: http://vela.localhost.com
      method: POST
      body: |
        This is a sample Vela plugin written with Kotlin
```
