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

Welcome to the Vela (VEE-la) tour! This tour covers the core components of building Vela pipelines. We will walk through the components that make up a pipeline and show how/where they are used inside a Vela YAML file (Can be `.vela.yml` or `.vela.yaml`).

Vela has a few core pipeline types steps, stages, and templates. Steps pipelines should be used in situations when everything in the workflow needs to be accomplished sequentially. Stages are pipelines that are leveraged when workflows can or need to run in parallel. Lastly, templates, the goal with these pipelines is to identify one too many tasks that can be abstracted and used repeatedly.

Vela pipelines execute commands inside ephemeral Docker containers. By integrating with Docker we provide isolation between steps and allow safe execution of concurrent tasks on the same machine. Using containers empowers users to customize the features and functionality they want Vela to perform through plugins.

A plugin is a Docker container that performs a pre-defined set of tasks and typically is configured as a step in pipelines. Plugins can be used to deploy code, publish artifacts, send notifications, and much more. Additionally, for even more powerful workflows you can string together a set of plugins into a single template to create reusable pipelines across your applications. Users can create one or many templates, to be stored in separate files, and then reference each template in the full pipeline configuration.

