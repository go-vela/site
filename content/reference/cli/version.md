---
title: "Version"
linkTitle: "Version"
weight: 16
description: >
  Learn how to get version information for the Vela CLI.
---

## Command

```
$ vela version
```

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).
To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
vela version
```

#### Response

```sh
{
  Canonical: v0.7.0,
  Major: 0,
  Minor: 7,
  Patch: 0,
  Metadata: {
    Architecture: amd64,
    BuildDate: 2021-02-01T15:40:21Z,
    Compiler: gc,
    GitCommit: 6225623858e09b7277f3d274d1ed75289a9eb549,
    GoVersion: go1.15.7,
    OperatingSystem: darwin,
  }
}
```
