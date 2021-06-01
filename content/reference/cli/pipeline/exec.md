---
title: "Exec"
linkTitle: "Exec"
description: >
  Learn how to execute a pipeline locally.
---

## Command

```
$ vela execute pipeline <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela exec pipeline --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name     | Description                                   | Environment Variables             |
| -------- | --------------------------------------------- | --------------------------------- |
| `branch` | the build branch for the pipeline             | `VELA_BRANCH`, `PIPELINE_BRANCH`  |
| `comment`| the build comment for the pipeline            | `VELA_COMMENT`, `PIPELINE_COMMENT`|
| `event`  | the build event for the pipeline              | `VELA_EVENT`, `PIPELINE_EVENT`    |
| `tag`    | the build tag for the pipeline                | `VELA_TAG`, `PIPELINE_TAG`        |
| `target` | the build target for the pipeline             | `VELA_TARGET`, `PIPELINE_TARGET`  |
| `output` | format the output in json, spew or yaml       | `VELA_OUTPUT`, `PIPELINE_OUTPUT`  |
| `file`   | name of the file for the pipeline             | `VELA_FILE`, `PIPELINE_FILE`      |
| `path`   | path to the file for the pipeline             | `VELA_PATH`, `PIPELINE_PATH`      |
| `local`  | enables mounting local directory to pipeline  | `VELA_LOCAL`, `PIPELINE_LOCAL`    |
| `volume` | provide list of local volumes to mount        | `VELA_VOLUMES`, `PIPELINE_VOLUMES`|
| `org`    | provide the organization for the pipeline     | `VELA_ORG`, `PIPELINE_ORG`        |
| `repo`   | provide the repository for the pipeline       | `VELA_REPO`, `PIPELINE_REPO`      |

## Secrets

The Vela Exec command does not have access to any secret you have stored in Vela or any other attached secret store.

You can set environment variables for the command by putting them before the command, ie `MY_SECRET=foo vela exec pipeline`. 

So if our pipeline is using the [kaniko plugin](https://go-vela.github.io/docs/plugins/registry/pipeline/kaniko/), it may require the secret `kaniko_password`, which we can provide with `KANIKO_PASSWORD=mypass vela exec pipeline`

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
vela exec pipeline
```

#### Response

```sh
[step: init] > Inspecting runtime network...
[step: init] $ docker network inspect localOrg_localRepo_1
{
 "Name": "localOrg_localRepo_1",
 "Id": "cf204e6081cd4c10e3a285e7545790152afca05991c2dc67534f496844c1d274",
 "Created": "2021-06-01T19:37:35.4772628Z",
 "Scope": "local",
 "Driver": "bridge",
 "EnableIPv6": false,
 "IPAM": {
  "Driver": "default",
  "Options": null,
  "Config": [
   {
    "Subnet": "192.168.0.0/20",
    "Gateway": "192.168.0.1"
   }
  ]
 },
 "Internal": false,
 "Attachable": false,
 "Ingress": false,
 "ConfigFrom": {
  "Network": ""
 },
 "ConfigOnly": false,
 "Containers": {},
 "Options": {},
 "Labels": {}
}

[step: init] > Inspecting runtime volume...
[step: init] $ docker volume inspect localOrg_localRepo_1
{
 "CreatedAt": "2021-06-01T19:37:35Z",
 "Driver": "local",
 "Labels": null,
 "Mountpoint": "/var/lib/docker/volumes/localOrg_localRepo_1/_data",
 "Name": "localOrg_localRepo_1",
 "Options": null,
 "Scope": "local"
}

[step: init] > Pulling service images...
[step: init] > Pulling stage images...
[step: init] > Pulling step images...
[step: init] $ docker image inspect alpine:latest
sha256:6dbb9cc54074106d46d4ccb330f2a40a682d49dda5f4844962b7dce9fe44aaec


[step: hello Vela] $ echo "hello Vela!"
[step: hello Vela] hello Vela!
```
