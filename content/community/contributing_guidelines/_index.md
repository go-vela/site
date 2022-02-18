---
title: "Contributing Guidelines"
toc: true
weight: 2
description: >
  Contributing Guidelines for Vela.
---

Thank you for considering contributing to [Vela](https://github.com/go-vela). Please read through these contributing guidelines.

# Vela project overview

## Types of project repos

### Core Repos

- [types](https://github.com/go-vela/types)
- [server](https://github.com/go-vela/server)
- [sdk-go](https://github.com/go-vela/sdk-go)
- [worker](https://github.com/go-vela/worker)
- [cli](https://github.com/go-vela/cli)
- [ui](https://github.com/go-vela/ui)

#### Core Repos Dependency Tree

Vela is written in a modular format which creates a dependency tree. The ui is independent.

```text
     ┌────────────┐   ┌────────────┐   ┌────────────┐   ┌────────────┐   ┌────────────┐
     │            │   │            │   │            │   │            │   │            │
     │            │   │            │   │            │   │            │   │            │
 ────┤   types    ├──►│   server   ├──►│   sdk-go   ├──►│   worker   ├──►│    cli     │
     │            │   │            │   │            │   │            │   │            │
     │            │   │            │   │            │   │            │   │            │
     └────────────┘   └────────────┘   └────────────┘   └────────────┘   └────────────┘


     ┌────────────────────────────────────────────────────────────────────────────────┐
     │                                                                                │
     │                                                                                │
 ────┤                                    ui                                          │
     │                                                                                │
     │                                                                                │
     └────────────────────────────────────────────────────────────────────────────────┘
```

### Plugin Repos
- Most [repos](https://github.com/go-vela) that start with `vela-` are plugin repos. They might have a dependency on a core repo. Check out the corresponding `go.mod` file to confirm.

### Supporting Repos
- [docs](https://github.com/go-vela/docs)
- [vela-tutorials](https://github.com/go-vela/vela-tutorials)
- [community](https://github.com/go-vela/community) (migrations, proposals, releases (release notes), [issues](/docs/communityy/contributing_guidelines/#issues))
- [homebrew](https://github.com/go-vela/homebrew) (brew tap go-vela/vela)

## Types of Contributions

### Issues

[Issues](https://github.com/go-vela/community/issues) include:
- Bugs
- Enhancements
- Feature requests

### Proposals

[Proposals](https://github.com/go-vela/community/tree/master/proposals) are used to foster discussion around large or breaking feature requests, or when looking for feedback on varied implementation options. Check that an [issue](https://github.com/go-vela/community/issues) or [proposal](https://github.com/go-vela/community/tree/master/proposals) doesn’t exist already.

Create a pull request using the [proposal template](https://github.com/go-vela/community/blob/master/.github/PULL_REQUEST_TEMPLATE/proposal.md).

Anyone is welcome to weigh in on a proposal. If you’d like, link it in the [public #vela Slack channel](https://gophers.slack.com/app_redirect?channel=CNRRKE8KY) for more visibility.

There isn’t a clearly defined proposal process yet (we’re working on that). We do monitor and engage on proposals to reach a consensus. If the proposal is approved to move forward, as indicated within the comments of the proposal pull request, the next step is to create a Feature Request for tracking purposes.

## Lifecycle of a Contribution

{{% alert title="Note:" color="warning" %}}
Make sure an [issue](https://github.com/go-vela/community/issues) or [proposal](https://github.com/go-vela/community/tree/master/proposals) in the [go-vela/community](https://github.com/go-vela/community) repository exists prior to beginning any code changes.
{{% /alert %}}

### Determining appropriateness for Vela
Before contributing any code, make sure an [issue](/docs/community/contributing_guidelines/#issues) exists, be sure to checkout current issues](https://github.com/go-vela/community/issues) and [proposals](https://github.com/go-vela/community/tree/master/proposals) to make sure your idea isn’t already being worked on. We're working on a public roadmap view to link here.

If an issue does not exist, make sure to create one.

Vela is Target’s primary CI system. We will evaluate issues and proposals, and compare them against our roadmap, what is best for Target, and what makes sense to implement for other customers that will provide a general positive value for other users.

### Project boards
Our [project boards](https://github.com/orgs/go-vela/projects) give you a detailed overview of what’s currently planned or being worked on. Each sprint reflects the stage in our roadmap we are focused on. 

Once your proposal or issue is approved, make sure your progress is being tracked in the current sprint.

### Categories / Labels 
Issues are sorted by using labels and categories (columns) in our backlog. This is to aid us in prioritization and planning.

Some common labels might be:
- Bug
- Enhancement
- Feature

Occasionally, we will use other labels to try and group similar bugs/features/enhancements into a common goal. For example, there might be a label, `observability`, that could contain bugs/features/enhancements that all pertain to observability. 

### Backlog Grooming
The Vela core team reviews issues in the community repo once a month. At this point we will determine whether issues fit into our roadmap, assess priority, and potentially close issues that will not be worked by the core team. 

### Development Workflow
Checkout the README.md in the repo you intend to contribute to, for instructions on how to setup your repo locally and start contributing.

See [style guide](/docs/community/contributing_guidelines/#style-guide) for guides on implementation.

- **Open a pull request!**
  * For the title of the pull request, please use the following format:

    ```text
    feat(wobble): add hat wobble
    ^--^^------^  ^------------^
    |   |         |
    |   |         +---> Summary in present tense.
    |   +---> Scope: a noun describing a section of the codebase (optional)
    +---> Type: chore, docs, feat, fix, refactor, or test.
    ```

    * feat: adds a new feature (equivalent to a MINOR in Semantic Versioning)
    * fix: fixes a bug (equivalent to a PATCH in Semantic Versioning)
    * docs: changes to the documentation
    * refactor: refactors production code, eg. renaming a variable; doesn’t change public API
    * test: adds missing tests, refactors tests; no production code change
    * chore: updates something without impacting the user (ex: bump a dependency in package.json or go.mod); no production code change

  * If a code change introduces a breaking change, place ! suffix after type, ie. feat(change)!: adds breaking change. correlates with MAJOR in semantic versioning.

  * If your code crosses dependent repos, link associated PRs in PR body.

- **PR review process**
  * Getting Reviewed: The admins and trusted committers actively watch for incoming PR’s.

  * Getting Approved: For [core repos](/docs/community/contributing_guidelines/#core-repos), PRs need 2 approvals. At least one approval must come from an admin, the other can be from a trusted committer. For plugin repos, 1 approval from an admin or trusted committer is needed.

  * Getting Merged: Once approved, your PR will be merged by an admin. If your story crosses dependent repos, PRs will be merged in the appropriate order neccessary.

## Releases
Vela is working to release on a consistent schedule. Our current goal is to release a new version once a month so users can work with the latest implemented features and bug fixes. Because Vela is in major version 0, breaking changes may happen on minor version releases. Once we release with major version > 0, [semantic versioning](https://semver.org/) will be followed.
Currently, main releases only apply to [core repos](/docs/community/contributing_guidelines/#core-repos). [Plugin repos](/docs/community/contributing_guidelines/#plugin-repos) get version cuts on an as needed basis.

- **Patches:** Patches will be released on an as needed basis for bug and security fixes. We increment the minor version.
- **RC’s (pre-releases):** Prior to releasing a main version, we will have at least a week of rc releases for testing purposes.
- **Release Notes:** You can find a list of release notes in the [community repository](https://github.com/go-vela/community/tree/master/releases).

## Style Guide
As you contribute to Vela, we ask that you follow these style guides to keep the code clean and consistent.

- **Git commit messages:** Ensure your commits follow our [standards](https://cbea.ms/git-commit/#seven-rules).

- **Linters:** We use [golangci-lint](https://golangci-lint.run/) to lint our code.  Make sure to run the provided style checks (make fmt, make tidy, etc.) against your code. Please address linter warnings appropriately. If you are intentionally violating a rule that triggers a linter, please annotate the respective code with nolint declarations [docs](https://golangci-lint.run/usage/false-positives/). We are using the following format for nolint declarations:

    ```go
    // nolint:<linter(s)> // <short reason>
    ```

    Example:

    ```go
    // nolint:gocyclo // legacy function is complex, needs simplification
    func superComplexFunction() error {
      // ..
    }
    ```

    Check the [documentation for more examples](https://golangci-lint.run/usage/false-positives/).

- **Documentation:** If your contribution warrants documentation within our [doc site](https://github.com/go-vela/docs), have a documentation PR ready and referenced in your code PR. Additionally, when contributing in a plugin repo, make sure to update the plugin’s documentation (DOCS.md) to reflect the change. 

- **Testing:** Make sure you add tests for the code you contribute. The total test coverage should never go down. Checkout the tests in the repo to get started. See [cypress](https://www.cypress.io/), [elm](https://package.elm-lang.org/packages/elm-explorations/test/latest/), and [golang](https://pkg.go.dev/testing) testing frameworks for more details. 

- **Folder structure:** Currently, we use a modified version of the [golang project folder structure](https://github.com/golang-standards/project-layout). When contributing to any repo, keep the structure consistent within the repo. When creating new plugins, be sure to mirror the structure of other plugins (vela-). 

- **Dependency management:** Check out the [core repos](/docs/community/contributing_guidelines/#dependency-tree-for-core-repos) and the [plugin repos](/docs/community/contributing_guidelines/#plugin-repos) to see how they are dependent on one another. We ask that you use standard libraries whenever possible. See [golang modules](https://go.dev/blog/using-go-modules) and [npm](https://docs.npmjs.com/about-npm) for dependency management.

- **Environment variables:** Add environment variables whenever implementation can vary by customer installation, or can be modified outside of a release.

- **Commenting:** Make sure to add comments to your code when necessary. Users should know what your code is doing by your comments. Check out comments in existing code to get a feel of what and how to comment.

- **Accessibility** Vela strives to conform to [Web Content Accessibility Guidelines 2.1](https://www.w3.org/TR/WCAG21/) AA standards for accessibility. Please ensure your contribution(s) meets or exceeds this standard.

## Roles
Because Vela is an open source tool, anyone can contribute! We have our admins and trusted committers defined in [teams](https://github.com/orgs/go-vela/teams).
- **Admins:** As admins of go-vela, members of this team work daily to keep Vela up and running. PRs will always need at least one admin approval.
- **Trusted committers:** This is a group of trusted individuals that are responsible for ushering our contributors into the world of Vela.
- **You:** Someone who wants to help make Vela the best CI tool out there!

## Questions and Contact
If you have a question about contributing to Vela, the above guidelines, or Vela in general, please reach out to the Vela team!
- [#vela](https://gophers.slack.com/app_redirect?channel=CNRRKE8KY) Slack channel
- Email us at [vela@target.com](mailto:vela@target.com)
- [Support resources](https://github.com/go-vela/ui/blob/master/.github/SUPPORT.md)
- Open an [issue](https://github.com/go-vela/community/issues/new/choose)
