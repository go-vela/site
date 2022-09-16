---
title: "Badges"
linkTitle: "Badges"
description: >
  Show off your build status.
---

{{% alert title="Note:" color="primary" %}}
These docs assume you have Vela running.
{{% /alert %}}

### How to get your badge

The server has an endpoint that will return an SVG badge for the default branch of your repo. The badge represents the current status for the most recent build for that branch. The most recent build refers to any build produced by the repo that is attached to that branch, which includes any event (push, pull request, etc).

```sh
# Syntax
https://<vela server>/badge/<org>/<repo>/status.svg

# Example
https://vela.example.com/badge/octocat/Hello-World/status.svg
```

In addition you can specify which branch you want to get a badge for by supplying a `?branch=` query parameter in the URL.

```sh
# Syntax
https://<vela server>/badge/<org>/<repo>/status.svg?branch=<branch name>

# Example
https://vela.example.com/badge/octocat/Hello-World/status.svg?branch=not_default
```

### Embedding in Markdown

To embed your badge in your markdown formatted file, follow this example:

```sh
# Syntax
[![Build Status](https://<vela server>/badge/<org>/<repo>/status.svg)](https://<vela server>/badge/<org>/<repo>)

# Example
[![Build Status](https://vela.example.com/badge/octocat/Hello-World/status.svg)](https://vela.example.com/badge/octocat/Hello-World)
```
