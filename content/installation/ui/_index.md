---
no_list: true
title: "UI Overview"
linkTitle: "UI"
weight: 3
description: >
  This section contains information on the Vela UI service.
---

Known as the user interface for the Vela application, often referred to as the Vela UI, this service provides a means for utilizing and interacting with the Vela platform.

The Vela UI aims to provide users with an easy-to-use toolbox that supplies most of the functionality necessary for managing, investigating, and successfully troubleshooting Vela pipelines.

This array of functionality includes viewing and managing resources in the system, enabling repositories, compiling pipelines, viewing logs etc. Most of these actions are performed through interacting with the server API on the user's behalf.

The UI also offers a quick glance into additional pipeline information, including any errors that might be interfering with the success of your pipeline, such as webhook processing issues returned by the SCM or user pipeline syntax mistakes. The purpose of the UI is to make managing and debugging Vela pipelines not only possible, but approachable.

## Deployment Guides

Vela supports a number of deployment strategies to enable the preferences of you and your team.

This section provides a list of comprehensive guides to install and start the UI:

### Docker

From the [Docker official website](https://docker.io/):

> Docker takes away repetitive, mundane configuration tasks and is used throughout the development lifecycle for fast, easy and portable application development - desktop and cloud. Docker’s comprehensive end to end platform includes UIs, CLIs, APIs and security that are engineered to work together across the entire application delivery lifecycle.

Please refer to [our Docker deployment guide](/docs/installation/ui/docker/) to get started.

### Kubernetes

From the [Kubernetes official website](https://kubernetes.io/):

> Kubernetes, also known as K8s, is an open-source system for automating deployment, scaling, and management of containerized applications.

Please refer to [our Kubernetes deployment guide](/docs/installation/ui/kubernetes/) to get started.