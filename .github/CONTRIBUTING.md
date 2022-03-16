# Contributing

## Getting Started

We'd love to accept your contributions to this project! If you are a first time contributor, please review our [Contributing Guidelines](https://go-vela.github.io/docs/community/contributing_guidelines/) before proceeding.

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

* Make sure to follow our [PR process](https://go-vela.github.io/docs/community/contributing_guidelines/#development-workflow) when opening a pull request

Thank you for your contribution!

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
