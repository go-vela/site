## Description

This plugin enables you to run [Terraform](https://www.terraform.io/) against [providers](https://www.terraform.io/docs/providers/index.html) in a Vela pipeline.

Source Code: https://github.com/go-vela/vela-terraform

Registry: https://hub.docker.com/r/target/vela-terraform

## Usage

**NOTE: by default Terraform runs in the current directory. Use `directory: path/to/tf/files` to point Terraform at a file or files.**

Sample of adding init options to Terraform configuration:

```yaml
- name: apply
  image: target/vela-terraform:latest
  pull: true
  parameters:
    action: apply
    auto_approve: true # Required for versions of Terraform 0.12.x
    init_options:
      get_plugins: true
```

Sample of applying Terraform configuration:

```yaml
- name: apply
  image: target/vela-terraform:latest
  pull: true
  parameters:
    action: apply
    auto_approve: true # Required for versions of Terraform 0.12.x
```

Sample of destroying Terraform configuration:

```yaml
- name: destroy
  image: target/vela-terraform:latest
  pull: true
  parameters:
    action: destroy
    auto_approve: true # Required for versions of Terraform 0.12.x
```

Sample of formatting Terraform configuration files:

```yaml
- name: fmt
  image: target/vela-terraform:latest
  pull: true
  parameters:
    action: fmt
```

Sample of planning Terraform configuration:

```yaml
- name: plan
  image: target/vela-terraform:latest
  pull: true
  parameters:
    action: plan
```

Sample of validating Terraform configuration:

```yaml
- name: validate
  image: target/vela-terraform:latest
  pull: true
  parameters:
    action: validate
```


## Secrets

**NOTE: Users should refrain from configuring sensitive information in their pipeline in plain text.**

```diff
- name: apply
  image: target/vela-terraform:latest
  pull: true
+  secrets: [ github_token ]
  parameters:
    action: apply
    auto_approve: true # Required for versions of Terraform 0.12.x
```

## Parameters

The following parameters are used to configure the image:

| Name           | Description                                 | Required | Default |
| -------------- | ------------------------------------------- | -------- | ------- |
| `action`       | action to perform with Terraform            | `true`   | `N/A`   |
| `directory`    | the directory for action to be performed on | `false`  | `N/A`   |
| `init_options` | options to use for Terraform init operation | `false`  | `N/A`   |
| `log_level`    | set the log level for the plugin            | `true`   | `info`  |


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

_Command uses Terraform CLI command defaults if not overridden in config._

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

_Command uses Terraform CLI command defaults if not overridden in config._

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

_Command uses Terraform CLI command defaults if not overridden in config._

| Name    | Description                                   | Required | Default |
| ------- | --------------------------------------------- | -------- | ------- |
| `check` | validate if the input is formatted            | `false`  | `N/A`   |
| `diff`  | diffs of formatting changes                   | `false`  | `N/A`   |
| `list`  | list files whose formatting differs           | `false`  | `N/A`   |
| `write` | write result to source file instead of STDOUT | `false`  | `N/A`   |

#### Plan

The following parameters are used to configure the `plan` action:

_Command uses Terraform CLI command defaults if not overridden in config._

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

_Command uses Terraform CLI command defaults if not overridden in config._

| Name              | Description                                                           | Required | Default |
| ----------------- | --------------------------------------------------------------------- | -------- | ------- |
| `check_variables` | command will check whether all required variables have been specified | `false`  | `N/A`   |
| `no_color`        | disables colors in output                                             | `false`  | `N/A`   |
| `vars`            | a map of variables to pass to the Terraform (`<key>=<value>`)         | `false`  | `N/A`   |
| `var_files`       | a list of var files to use                                            | `false`  | `N/A`   |

## Template

COMING SOON!

## Troubleshooting

Below are a list of common problems and how to solve them:

_How do I add verbose logging to the Terraform CLI?_

```diff
- name: apply
 image: docker.target.com/rapid/neal/vela-terraform
 pull: true
#  Verbose Terraform logging can be added directly to environment
+ environment:
+   TF_LOG: TRACE
 parameters:
   action: apply   
   auto_approve: true
```
