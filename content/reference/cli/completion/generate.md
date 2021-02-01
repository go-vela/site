---
title: "Generate"
linkTitle: "Generate"
description: >
  Learn how to produce auto-completion for your terminal.
---

## Command

```
$ vela generate completion <parameters...> <arguments...>
```

{{% alert color="info" %}}
For more information, you can run `vela generate completion --help`.
{{% /alert %}}

## Parameters

The following parameters are used to configure the command:

| Name   | Description                            | Environment Variables          |
| ------ | -------------------------------------- | ------------------------------ |
| `bash` | generate a Bash auto-completion script | `VELA_BASH`, `COMPLETION_BASH` |
| `zsh`  | generate a Zsh auto-completion script  | `VELA_ZSH`, `COMPLETION_ZSH`   |

## Permissions

COMING SOON!

## Sample

{{% alert color="warning" %}}
This section assumes you have already installed and setup the CLI.

To install the CLI, please review the [installation documentation](/docs/reference/cli/install/).

To setup the CLI, please review the [authentication documentation](/docs/reference/cli/authentication/).
{{% /alert %}}

#### Request

```sh
vela generate completion --bash
```

#### Response

```sh
#! /bin/bash

_cli_bash_autocomplete() {
  if [[ "${COMP_WORDS[0]}" != "source" ]]; then
    local cur opts base
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"

    if [[ "$cur" == "-"* ]]; then
      opts=$( ${COMP_WORDS[@]:0:$COMP_CWORD} ${cur} --generate-bash-completion )
    else
      opts=$( ${COMP_WORDS[@]:0:$COMP_CWORD} --generate-bash-completion )
    fi

    COMPREPLY=( $(compgen -W "${opts}" -- ${cur}) )
      return 0
  fi
}

complete -o bashdefault -o default -o nospace -F _cli_bash_autocomplete vela
```

## Permanent Automatic Completion

This section covers how to enable auto-completion for your terminal permanently.

#### Bash

{{% alert color="info" %}}
This section assumes you have a version of Bash greater than 4.

You can check your Bash version with:

```sh
bash --version
```

If you have a version older than 4, you can use [brew](https://brew.sh) to install a newer version.

```sh
brew install bash
```
{{% /alert %}}

1. Install v2 of Bash Completion

```sh
brew install bash-completion@2
```

2. Copy Vela Bash Completion script

```sh
vela generate completion --bash >> /usr/local/etc/bash_completion.d/vela.sh
```

3. Update Bash Profile with Completion

```sh
export BASH_COMPLETION_COMPAT_DIR="/usr/local/etc/bash_completion.d" >> $HOME/.bash_profile
[[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh" >> $HOME/.bash_profile
```

4. Source Bash Profile in Current Terminal

```sh
source $HOME/.bash_profile
```

#### Zsh

1. Update Zsh Profile with Completion

```sh
source <(vela generate completion --zsh) >> $HOME/.zshrc
```

{{% alert color="info" %}}
If you're met with an error like:

```sh
complete:13: command not found: compdef
```

Then you need to add the following to the top of your `$HOME/.zshrc`:

```sh
autoload -Uz compinit
compinit
```
{{% /alert %}}
