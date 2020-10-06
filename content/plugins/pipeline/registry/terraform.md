---
title: "Terraform"
---

## Description

This plugin enables you to run [Terraform](https://www.terraform.io/) against [providers](https://www.terraform.io/docs/providers/index.html) in a Vela pipeline.

Source Code: https://github.com/go-vela/vela-terraform

Registry: https://hub.docker.com/r/target/vela-terraform

## Usage

{{% alert color="warning" %}}
Users should refrain from using `latest` as the tag for the Docker image.

It is recommended to use a semantically versioned tag instead.
{{% /alert %}}

Sample of adding init options to Terraform configuration:

```yaml
steps:
  - name: apply
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: apply
      auto_approve: true # Required for versions of Terraform 0.12.x
      init_options:
        get_plugins: true
```

Sample of applying Terraform configuration:

```yaml
steps:
  - name: apply
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: apply
      auto_approve: true # Required for versions of Terraform 0.12.x
```

Sample of destroying Terraform configuration:

```yaml
steps:
  - name: destroy
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: destroy
      auto_approve: true # Required for versions of Terraform 0.12.x
```

Sample of formatting Terraform configuration files:

```yaml
steps:
  - name: fmt
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: fmt
```

Sample of planning Terraform configuration:

```yaml
steps:
  - name: plan
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: plan
```

Sample of validating Terraform configuration:

```yaml
steps:
  - name: validate
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: validate
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.
{{% /alert %}}

### Internal

The plugin accepts the following `parameters` for authentication:

| Parameter        | Environment Variable Configuration                                |
| ---------------- | ----------------------------------------------------------------- |
| `netrc_password` | `GIT_PASSWORD`, `PARAMETER_NETRC_PASSWORD`, `VELA_NETRC_PASSWORD` |
| `netrc_username` | `GIT_USERNAME`, `PARAMETER_NETRC_USERNAME`, `VELA_NETRC_USERNAME` |

Users can use [Vela internal secrets](/docs/concepts/pipeline/secrets/) to substitute sensitive values at runtime:

```diff
steps:
  - name: plan
    image: target/vela-terraform:latest
    pull: always
+   secrets: [ git_username, git_password ]
    parameters:
      action: plan
-     netrc_username: octocat
-     netrc_password: superSecretPassword
```

{{% alert color="info" %}}
This example will add the `secrets` to the `plan` step as environment variables:

- `GIT_USERNAME=<value>`
- `GIT_PASSWORD=<value>`
{{% /alert %}}

### External

The plugin accepts the following files for authentication:

| Parameter        | Volume Configuration                                                                  |
| ---------------- | ------------------------------------------------------------------------------------- |
| `netrc_password` | `/vela/parameters/terraform/netrc/password`, `/vela/secrets/terraform/netrc/password` |
| `netrc_username` | `/vela/parameters/terraform/netrc/username`, `/vela/secrets/terraform/netrc/username` |

Users can use [Vela external secrets](/docs/concepts/pipeline/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: plan
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: plan
-     netrc_username: octocat
-     netrc_password: superSecretPassword
```

{{% alert color="info" %}}
This example will read the secrets values in the volume stored at `/vela/secrets/`:
{{% /alert %}}

## Parameters

{{% alert color="info" %}}
The plugin supports reading all parameters vie environment variables or files.

Any values set from a file take precedence over values set from the environment.

By default, Terraform runs in the current directory - use `directory: path/to/tf/files` to point Terraform at a file or files.

Terraform ships with a default version but you can download the specific version you need with `version: x.x.x`
{{% /alert %}}

The following parameters are used to configure the image:

| Name           | Description                                 | Required | Default |
| -------------- | ------------------------------------------- | -------- | ------- |
| `action`       | action to perform with Terraform            | `true`   | `N/A`   |
| `directory`    | the directory for action to be performed on | `false`  | `N/A`   |
| `init_options` | options to use for Terraform init operation | `false`  | `N/A`   |
| `log_level`    | set the log level for the plugin            | `true`   | `info`  |
| `version`      | set the Terraform CLI version               | `true`   | `info`  |

The following parameters can be used within the `init_options` to configure the image:

| Name              | Description                                                                           | Required | Default |
| ----------------- | ------------------------------------------------------------------------------------- | -------- | ------- |
| `backend`         | configure the backend for this configuration                                          | `true`   | `N/A`   |
| `backend_configs` | this is merged with what is in the configuration file                                 | `true`   | `N/A`   |
| `force_copy`      | suppress prompts about copying state data                                             | `true`   | `N/A`   |
| `from_module`     | copy the contents of the given module into the target directory before initialization | `true`   | `N/A`   |
| `get`             | download any modules for this configuration                                           | `true`   | `N/A`   |
| `get_plugins`     | download any missing plugins for this configuration                                   | `true`   | `N/A`   |
| `input`           | ask for input for variables if not directly set                                       | `true`   | `N/A`   |
| `lock`            | lock the state file when locking is supported                                         | `false`  | `N/A`   |
| `lock_timeout`    | duration to retry a state lock                                                        | `false`  | `N/A`   |
| `no_color`        | disables colors in output                                                             | `false`  | `N/A`   |
| `plugin_dirs`     | directory containing plugin binaries; overrides all default search paths for plugins  | `false`  | `N/A`   |
| `reconfigure`     | reconfigure the backend, ignoring any saved configuration                             | `false`  | `N/A`   |
| `upgrade`         | install the latest version allowed within configured constraints                      | `false`  | `N/A`   |
| `verify_plugins`  | verify the authenticity and integrity of automatically downloaded plugins             | `false`  | `N/A`   |

#### Apply

The following parameters are used to configure the `apply` action:

{{% alert color="warning" %}}
This action uses the Terraform CLI command defaults if not explicitly set.
{{% /alert %}}

| Name           | Description                                                   | Required | Default |
| -------------- | ------------------------------------------------------------- | -------- | ------- |
| `auto_approve` | skip interactive approval of running command                  | `false`  | `N/A`   |
| `back_up`      | path to backup the existing state file                        | `false`  | `N/A`   |
| `directory`    | the directory for action to be performed on                   | `false`  | `N/A`   |
| `lock`         | lock the state file when locking is supported                 | `false`  | `N/A`   |
| `lock_timeout` | duration to retry a state lock                                | `false`  | `N/A`   |
| `no_color`     | disables colors in output                                     | `false`  | `N/A`   |
| `parallelism`  | number of concurrent operations as Terraform walks its graph  | `false`  | `N/A`   |
| `refresh`      | update state prior to checking for differences                | `false`  | `N/A`   |
| `state`        | path to read and save state                                   | `false`  | `N/A`   |
| `state_out`    | path to write updated state file                              | `false`  | `N/A`   |
| `target`       | resource to target                                            | `false`  | `N/A`   |
| `vars`         | a map of variables to pass to the Terraform (`<key>=<value>`) | `false`  | `N/A`   |
| `var_files`    | a list of var files to use                                    | `false`  | `N/A`   |

#### Destroy

The following parameters are used to configure the `destroy` action:

{{% alert color="warning" %}}
This action uses the Terraform CLI command defaults if not explicitly set.
{{% /alert %}}

| Name           | Description                                                   | Required | Default |
| -------------- | ------------------------------------------------------------- | -------- | ------- |
| `auto_approve` | skip interactive approval of running command                  | `false`  | `N/A`   |
| `back_up`      | path to backup the existing state file                        | `false`  | `N/A`   |
| `lock`         | lock the state file when locking is supported                 | `false`  | `N/A`   |
| `lock_timeout` | duration to retry a state lock                                | `false`  | `N/A`   |
| `no_color`     | disables colors in output                                     | `false`  | `N/A`   |
| `parallelism`  | number of concurrent operations as Terraform walks its graph  | `false`  | `N/A`   |
| `refresh`      | update state prior to checking for differences                | `false`  | `N/A`   |
| `state`        | path to read and save state                                   | `false`  | `N/A`   |
| `state_out`    | path to write updated state file                              | `false`  | `N/A`   |
| `target`       | resource to target                                            | `false`  | `N/A`   |
| `vars`         | a map of variables to pass to the Terraform (`<key>=<value>`) | `false`  | `N/A`   |
| `var_files`    | a list of var files to use                                    | `false`  | `N/A`   |

#### Format

The following parameters are used to configure the `fmt` action:

{{% alert color="warning" %}}
This action uses the Terraform CLI command defaults if not explicitly set.
{{% /alert %}}

| Name    | Description                                   | Required | Default |
| ------- | --------------------------------------------- | -------- | ------- |
| `check` | validate if the input is formatted            | `false`  | `N/A`   |
| `diff`  | diffs of formatting changes                   | `false`  | `N/A`   |
| `list`  | list files whose formatting differs           | `false`  | `N/A`   |
| `write` | write result to source file instead of STDOUT | `false`  | `N/A`   |

#### Plan

The following parameters are used to configure the `plan` action:

{{% alert color="warning" %}}
This action uses the Terraform CLI command defaults if not explicitly set.
{{% /alert %}}

| Name                 | Description                                                        | Required | Default |
| -------------------- | ------------------------------------------------------------------ | -------- | ------- |
| `destroy`            | destroy all resources managed by the given configuration and state | `false`  | `N/A`   |
| `detailed_exit_code` | return detailed exit codes when the command exits                  | `false`  | `N/A`   |
| `lock`               | lock the state file when locking is supported                      | `false`  | `N/A`   |
| `lock_timeout`       | duration to retry a state lock                                     | `false`  | `N/A`   |
| `module_depth`       | specifies the depth of modules to show in the output               | `false`  | `N/A`   |
| `no_color`           | disables colors in output                                          | `false`  | `N/A`   |
| `parallelism`        | number of concurrent operations as Terraform walks its graph       | `false`  | `N/A`   |
| `refresh`            | update state prior to checking for differences                     | `false`  | `N/A`   |
| `state`              | path to read and save state                                        | `false`  | `N/A`   |
| `state_out`          | path to write updated state file                                   | `false`  | `N/A`   |
| `target`             | resource to target                                                 | `false`  | `N/A`   |
| `vars`               | a map of variables to pass to the Terraform (`<key>=<value>`)      | `false`  | `N/A`   |
| `var_files`          | a list of var files to use                                         | `false`  | `N/A`   |

#### Validate

The following parameters are used to configure the `validate` action:

{{% alert color="warning" %}}
This action uses the Terraform CLI command defaults if not explicitly set.
{{% /alert %}}

| Name              | Description                                                           | Required | Default |
| ----------------- | --------------------------------------------------------------------- | -------- | ------- |
| `check_variables` | command will check whether all required variables have been specified | `false`  | `N/A`   |
| `no_color`        | disables colors in output                                             | `false`  | `N/A`   |
| `vars`            | a map of variables to pass to the Terraform (`<key>=<value>`)         | `false`  | `N/A`   |
| `var_files`       | a list of var files to use                                            | `false`  | `N/A`   |

## Template

COMING SOON!

## Troubleshooting

{{% alert color="warning" %}}
We recommend reviewing Terraform's [debugging guide](https://www.terraform.io/docs/internals/debugging.html) before troubleshooting further.
{{% /alert %}}

You can start troubleshooting this plugin by tuning the level of logs being displayed:

```diff
steps:
  - name: apply
    image: target/vela-terraform:latest
    pull: always
    parameters:
      action: apply
      auto_approve: true # Required for versions of Terraform 0.12.x
      init_options:
        get_plugins: true
+     log_level: trace
```

Below are a list of common problems and how to solve them:

COMING SOON!
