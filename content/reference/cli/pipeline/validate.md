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

| Name                    | Description                                                  | Environment Variables                                 |
| ----------------------- | ------------------------------------------------------------ | ----------------------------------------------------- |
| `file`                  | name of the file for the pipeline                            | `VELA_FILE`, `PIPELINE_FILE`                          |
| `path`                  | path to the file for the pipeline                            | `VELA_PATH`, `PIPELINE_PATH`                          |
| `ref`                   | repository reference for the pipeline                        | `VELA_REF`, `PIPELINE_REF`                            |
| `template`              | enables templates to be included in pipeline validation      | `VELA_TEMPLATE`, `PIPELINE_TEMPLATE`                  |
| `template-file`         | enables using a local template file for expansion            | `VELA_TEMPLATE_FILE`, `PIPELINE_TEMPLATE_FILE`        |
| `remote`                | enables validating a pipeline on a remote server             | `VELA_REMOTE`, `PIPELINE_REMOTE`                      |
| `compiler.github.token` | github compiler token                                        | `VELA_COMPILER_GITHUB_TOKEN`, `COMPILER_GITHUB_TOKEN` |
| `compiler.github.url`   | github url, used by compiler, for pulling registry templates | `VELA_COMPILER_GITHUB_URL`, `COMPILER_GITHUB_URL`     |
| `pipeline-type`         | provide the repository pipeline type                         | `VELA_PIPELINE_TYPE`, `PIPELINE_TYPE`  |

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