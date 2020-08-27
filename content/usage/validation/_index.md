---
title: "Validation"
linkTitle: "Validation"
weight: 3
description: >
  Validating your pipeline.
---

Vela supports multiple ways to provide pipeline validation and feedback.

## Editors/IDEs

Integration with editors can enhance your pipeline writing experience by providing autocompletion, inline documentation, and links to documentation within your editor.

Many editors are supported out-of-the-box due to the inclusion of Vela's schema in the JSON Schema Store. However, _some_ editors might require manual configuration. You can leverage the [schema details on the schema page](/docs/usage/validation/schema/) to assist with that.

Select editors are also supported by their own plugin/extension ecosystems, which often include Yaml/JSON schema validator plugins with support for automatically pulling from the Schema Store. Search your editor's respective store/marketplace for an applicable extension.

Here are some examples for configuring certain editors without out-of-the-box support:

### Vim

Prerequisite:

- coc: https://github.com/neoclide/coc.nvim

Plugin:

- coc-yaml: https://github.com/neoclide/coc-yaml

### Visual Studio Code

Although support for `.json` files is built-in, an extension is needed to add the support for YAML files. The _YAML Language Support_ extension has been known to work well and requires no additional configuration.

Extension:

- YAML Language Support (`redhat.vscode-yaml`)

### Others

(open a PR to add your own)

## CLI

The [Vela CLI](/docs/cli/) offers a [validate command](/docs/cli/pipeline/validate/) to perform basic Yaml validation of your pipeline.

## UI

In the UI, you will receive validation information on malformed pipelines on the _Hooks_ (`<vela web url>/<org>/<repo>/hooks`) page for the respective git repository.
