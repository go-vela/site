---
title: "Overview"
linkTitle: "Overview"
description: >
  Learn about the kinds of Vela plugins.
---

{{% alert title="Note:" color="primary" %}}
Before you begin your plugin journey we recommend the following pre-requisites:

* [Steps](/docs/concepts/pipeline/steps/)
* [Stages](/docs/concepts/pipeline/stages/)
* [Templates](/docs/concepts/pipeline/templates/)
{{% /alert %}}

## Pipeline

These plugins are designed to be used within steps, stages and template pipelines. Pipeline plugins work via environment variables that pass data from pipeline to the container at runtime. 

A pipeline plugin is a Docker container that is designed to perform a set of pre-defined actions.

These actions can be for any number of general tasks, including:

* deploying code
* publishing artifacts
* sending notifications
* much, much more...

## Secret

Coming Soon!