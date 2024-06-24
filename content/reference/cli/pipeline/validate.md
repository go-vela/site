---
title: "Validate"
linkTitle: "Validate"
description: >
  Learn how to validate a Vela pipeline.
---

## Command

```
$ vela validate pipeline <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, please run `vela validate pipeline --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name                           | Description                                                                           | Environment Variables                                               |
| ------------------------------ | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `org`                          | name of organization for the builds                                                   | `VELA_ORG`, `BUILD_ORG`                                             |
| `pipeline-type`                | provide the repository pipeline type                                                  | `VELA_PIPELINE_TYPE`, `PIPELINE_TYPE`                               |
| `repo`                         | name of repository for the builds                                                     | `VELA_REPO`, `BUILD_REPO`                                           |
| `compiler-starlark-exec-limit` | set the starlark execution step limit for compiling starlark pipelines (default 7500) | `VELA_COMPILER_STARLARK_EXEC_LIMIT`, `COMPILER_STARLARK_EXEC_LIMIT` |
| `file`                         | name of the file for the pipeline                                                     | `VELA_FILE`, `PIPELINE_FILE`                                        |
| `max-template-depth`           | set the maximum depth for nested templates (default: 3)                               | `VELA_MAX_TEMPLATE_DEPTH`, `MAX_TEMPLATE_DEPTH`                     |
| `path`                         | path to the file for the pipeline                                                     | `VELA_PATH`, `PIPELINE_PATH`                                        |
| `ref`                          | repository reference for the pipeline                                                 | `VELA_REF`, `PIPELINE_REF`                                          |
| `remote`                       | enables validating a pipeline on a remote server                                      | `VELA_REMOTE`, `PIPELINE_REMOTE`                                    |
| `template`                     | enables templates to be included in pipeline validation                               | `VELA_TEMPLATE`, `PIPELINE_TEMPLATE`                                |
| `template-file`                | enables using a local template file for expansion                                     | `VELA_TEMPLATE_FILE`, `PIPELINE_TEMPLATE_FILE`                      |
| `branch`                       | provide the build branch for the pipeline                                             | `VELA_BRANCH`, `PIPELINE_BRANCH`, `VELA_BUILD_BRANCH`               |
| `comment`                      | provide the build comment for the pipeline                                            | `VELA_COMMENT`, `PIPELINE_COMMENT`, `VELA_BUILD_COMMENT`            |
| `event`                        | provide the build event for the pipeline                                              | `VELA_EVENT`, `PIPELINE_EVENT`, `VELA_BUILD_EVENT`                  |
| `file-changeset`               | provide a list of files changed for ruleset matching                                  | `VELA_FILE_CHANGESET`, `FILE_CHANGESET`                             |
| `status`                       | provide the expected build status for the local validation (default: "success")       | `VELA_STATUS`, `PIPELINE_STATUS`, `VELA_BUILD_STATUS`               |
| `tag`                          | provide the build tag for the pipeline                                                | `VELA_TAG`, `PIPELINE_TAG`, `VELA_BUILD_TAG`                        |
| `target`                       | provide the build target for the pipeline                                             | `VELA_TARGET`, `PIPELINE_TARGET`, `VELA_BUILD_TARGET`               |
| `clone-image`                  | the clone image to use for the injected clone step                                    | `VELA_CLONE_IMAGE`, `COMPILER_CLONE_IMAGE`                          |
| `compiler.github.token`        | github compiler token                                                                 | `VELA_COMPILER_GITHUB_TOKEN`, `COMPILER_GITHUB_TOKEN`               |
| `compiler.github.url`          | github url, used by compiler, for pulling registry templates                          | `VELA_COMPILER_GITHUB_URL`, `COMPILER_GITHUB_URL`                   |

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).
To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Simple Request

```sh
vela validate pipeline
```

#### Expanded Template Request (GitHub)

```sh
vela validate pipeline --template --compiler.github.token <token> --compiler.github.url https://git.example.com
```

#### Expanded Template Request (Local)

```sh
vela validate pipeline --template --template-file name:/path/to/file
```

#### Response

```sh
".vela.yml" is valid
```

Using a template in your pipeline? You can [validate templates also](/docs/templates/working_with/#cli-pipeline-validation).
