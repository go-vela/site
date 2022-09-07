---
title: "Overview"
linkTitle: "Installation"
layout: installation
description: >
  This section contains information on installing and administering Vela.
menu:
  main:
    weight: 5
---

{{% alert title="Tip:" color="primary" %}}
For information on how to install the Vela CLI, please check the [CLI Installation documentation](https://go-vela.github.io/docs/reference/cli/install/).
{{% /alert %}}

Vela is an open-source, Pipeline Automation ([CI/CD](https://www.redhat.com/en/topics/devops/what-is-ci-cd)) platform built on [Linux container](https://linuxcontainers.org/) technology.

A Vela cluster is deployed as a self-hosted solution and consists of two core services, the [server](/docs/installation/server/) and the [worker](/docs/installation/worker/). The relationship between these services is considered many-to-many meaning many workers can connect to many servers.

The server is considered the brains of the application while the worker is considered the brawn of the application.

An optional third service, the [UI](/docs/installation/ui/), can also be deployed but is not required for the Vela platform to operate as intended. This service provides a means for utilizing and interacting with the Vela platform.

![Vela Overview](vela.png)

## Services

There are 3 core services that make up Vela:
