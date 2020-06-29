---
title: "ZSH completion"
linkTitle: "ZSH completion"
description: >
  Enable zsh auto completion for vela-cli permanently
---

### Step 1 - Add the following to your ~/.zshrc

```
source <(vela completion zsh)
```

### Note

If you get an error like complete:13: command not found: compdef, then add the following to the beginning of your ~/.zshrc file:

```
autoload -Uz compinit
compinit
```
