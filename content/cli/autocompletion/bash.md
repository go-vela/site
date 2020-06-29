---
title: "Bash completion"
linkTitle: "Bash completion"
description: >
  Enable bash auto completion for vela-cli permanently
---

## Upgrade Bash

Instructions here are assumed to be executed in Bash version 4+. You can check your bash version by executing
```
echo $BASH_VERSION
```

if the version is older than 4, you can install new bash version using brew.
```
brew install bash
```

please visit https://brew.sh to install brew if you have not installed it already.

### Step 1 - Install bash completion v2

```
brew install bash-completion@2
```

### Step 2 - Copy vela completion script

```
vela completion bash >> /usr/local/etc/bash_completion.d/vela.sh
```

### Step 3 - Add the following to your ~/.bash_profile

```
export BASH_COMPLETION_COMPAT_DIR="/usr/local/etc/bash_completion.d"
[[ -r "/usr/local/etc/profile.d/bash_completion.sh" ]] && . "/usr/local/etc/profile.d/bash_completion.sh"
```

### Step 4 - Reload your shell OR source your bash profile in the same session

```
source ~/.bash_profile
```
