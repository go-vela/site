# Contributing

We'd love to accept your contributions to this project! There are just a few guidelines you need to follow.

## Bugs

Bug reports should be opened up as [issues](https://help.github.com/en/github/managing-your-work-on-github/about-issues) on the [go-vela/community](https://github.com/go-vela/community) repository!

## Feature Requests

Feature Requests should be opened up as [issues](https://help.github.com/en/github/managing-your-work-on-github/about-issues) on the [go-vela/community](https://github.com/go-vela/community) repository!

## Pull Requests

**NOTE: We recommend you start by opening a new issue describing the bug or feature you're intending to fix. Even if you think it's relatively minor, it's helpful to know what people are working on.**

We are always open to new PRs! You can follow the below guide for learning how you can contribute to the project!

## Getting Started

### Prerequisites

* [Review the commit guide we follow](https://chris.beams.io/posts/git-commit/#seven-rules) - ensure your commits follow our standards
* [Hugo](https://gohugo.io/getting-started/installing/) - building block for local development

### Setup

* [Fork](/fork) this repository

* Clone this repository to your workstation:

```bash
# Clone the project
git clone git@github.com:go-vela/docs.git $HOME/go-vela/docs
```

* Navigate to the repository code:

```bash
# Change into the project directory
cd $HOME/go-vela/docs
```

* Point the original code at your fork:

```bash
# Add a remote branch pointing to your fork
git remote add fork https://github.com/your_fork/docs
```

## Running the website locally

We use [Hugo](https://github.com/gohugoio/hugo) to build our site.

You will need to install:

- [Hugo](https://github.com/gohugoio/hugo)
- [Docsy](https://www.docsy.dev/docs/getting-started) theme for Hugo

Docsy has some of it's own requirements, listed in their getting started docs.

- [PostCSS](https://www.docsy.dev/docs/getting-started/#install-postcss)
- `git submodule update --init --recursive` to update the submodule

Once you've got that taken care of, from the repo root folder, run:

```
hugo server -w
```
