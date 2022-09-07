---
no_list: true
title: "Server Overview"
linkTitle: "Server"
weight: 1
description: >
  This section contains information on the Vela server service.
---

Known as the brains of the Vela application, this service is responsible for managing the state of application resources.

This includes managing resources in the system (repositories, users etc.) and storing resource data in the database.

Additionally, the server responds to event-driven requests (webhooks) which creates new builds to run on a [worker](/docs/installation/worker/).

After a build is created, it is pushed to the queue which will be retrieved and executed by a worker.

As a build is run by a worker, it will send requests to the server's API which stores the state of the build in the database.

![Build Workflow](/docs/installation/server/build_workflow.png)

## Deployment Guides

Vela supports a number of deployment strategies to enable the preferences of you and your team.

This section provides a list of comprehensive guides to install and start the server:

### Docker

From the [Docker official website](https://docker.io/):

> Docker takes away repetitive, mundane configuration tasks and is used throughout the development lifecycle for fast, easy and portable application development - desktop and cloud. Docker’s comprehensive end to end platform includes UIs, CLIs, APIs and security that are engineered to work together across the entire application delivery lifecycle.

Please refer to [our Docker deployment guide](/docs/installation/server/docker/) to get started.

### Kubernetes

From the [Kubernetes official website](https://kubernetes.io/):

> Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.

Please refer to [our Kubernetes deployment guide](/docs/installation/server/kubernetes/) to get started.
