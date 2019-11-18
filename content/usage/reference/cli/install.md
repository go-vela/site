---
title: "Install"
weight: 5
description: >
  Learn how to install the CLI.
---

Instructions are OS-specific, please keep in mind the OS when referring to the installation instructions below.

### MacOS

_[brew](https://brew.sh/) is the recommend install path_

#### Homebrew

```sh
# add Vela tap to your brew configuration
brew tap go-vela/vela

# update your your taps
brew update

# install Vela CLI
brew install vela
```

#### cURL

```sh
# download the binary
curl -L https://github.com/go-vela/cli/releases/download/v0.1.5/vela_darwin_amd64.tar.gz | tar zx

# copy binary to $PATH
sudo cp vela /usr/local/bin/
```

### Linux

#### cURL

```sh
# download the binary
curl -L https://github.com/go-vela/cli/releases/download/v0.1.5/vela_linux_amd64.tar.gz | tar zx

# copy binary to $PATH
sudo cp vela /usr/local/bin/
```

### Microsoft Windows

#### cURL

Note: `curl` must be installed differently

##### Command Prompt

```sh
# download the binary
curl -L https://github.com/go-vela/cli/releases/download/v0.1.5/vela_windows_amd64.tar.gz --output vela_windows_amd64.tar.gz
# unzipping the tarball
tar xzvf vela_windows_amd64.tar.gz
# copy binary to $PATH
copy vela C:\Windows\System32/vela.exe
```

##### Windows PowerShell

```sh
# download the binary
curl https://github.com/go-vela/cli/releases/download/v0.1.5/vela_windows_amd64.tar.gz -OutFile vela_windows_amd64.tar.gz
# unzipping the tarball
tar xzvf vela_windows_amd64.tar.gz
# copy binary to $PATH
cp vela C:\Windows\System32/vela.exe
```

##### PowerShell 6 (PowerShell Core)

```sh
# download the binary
curl -L https://github.com/go-vela/cli/releases/download/v0.1.5/vela_windows_amd64.tar.gz --output vela_windows_amd64.tar.gz
# unzipping the tarball
tar xzvf vela_windows_amd64.tar.gz
# copy binary to $PATH
cp vela C:\Windows\System32/vela.exe
```

### From Source

Source installation is intended **only developers and advanced users**.

If you do not have a working Golang environment, please follow [How to install Golang](https://golang.org/doc/install).

```sh
# download the repo
go get -d github.com/go-vela/cli

# change to the cli directory
cd ${GOPATH}/src/github.com/go-vela/cli

# build a release binary with Go
go build -o releases/vela

# move binary to user directory for execution
sudo mv releases/vela /usr/local/bin/vela
```
