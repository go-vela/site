---
title: "Tour"
linkTitle: "Tour"
layout: tour
description: >
  This section contains information on the components for Vela.
menu:
  main:
    weight: 105
---

Welcome to the Vela tour! The tour covers the core components of building Vela pipelines. We will walk through the core components that make up a pipeline and show how/where they are used inside a Vela YAML file (Can be `.vela.yml` or `.vela.yaml`). Vela pipelines execute pipeline commands inside ephemeral Docker containers. Docker containers provide isolation, allowing safe execution of concurrent pipelines on the same machine.

Vela has two core pipeline types steps, and stages. Steps pipelines should be used for use cases when everything in the build workflow need to be done sequentially. Stages are pipelines that are designed to run one to many steps workflows in parallel

Using containers empowers users to customize the features and functionality they want Vela to perform through plugins. A plugin is a Docker container that performs a pre-defined set of tasks and typically is configured as a step in pipelines. Plugins can be used to deploy code, publish artifacts, send notifications, and much more.

Vela also enables users to build simple, reusable pipelines with atlas templates. An atlas template is like creating an alias to a subset of a pipeline that can contain any number of steps you would like to execute. Users can create one or many atlas templates, to be stored in separate files, and then reference each template in the full pipeline configuration.

