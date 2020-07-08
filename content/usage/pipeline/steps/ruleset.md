---
title:  "Ruleset"
toc:  true
weight:  2
description: >
  Limit when your step will run.
---

The `ruleset` declaration for a build step instructs Vela what set of rules (conditions) to execute a step under. These rules limit the execution of the step at runtime and, if all rules in the ruleset evaluate to true, the step is executed; otherwise it is skipped.

```diff
version: "1"

steps:
  - name: test
    image: golang
+   ruleset:
+     branch: master
+     event: push
    commands:
      - go test ./...
```

This ruleset would limit the execution of the step to if the build branch is `master` and the build event triggered is a `push` event. Below is a description of all rule types to trigger off of as well as how to configure them.

### Branch

This rule type limits the execution of a step to **matching build branches**. The below example will run a step if the build branch is `stage` or `master`:

```yaml
ruleset:
  branch: [ stage, master ]
```

### Event

This rule type limits the execution of a step to **matching build events**. The below example will run a step if the build event is `push` or `pull_request`:

```yaml
ruleset:
  event: [ push, pull_request ]
```

### Status

This rule type limits the execution of a step to **matching build statuses**. The below example will run a step if the build status is `failure` or `success`:

```yaml
ruleset:
  status: [ failure, success ]
```

### Continue

This rule type limits the execution of a step to **continuing on any failure**. The below example will run a step if `continue` is set to `true`:

```yaml
ruleset:
  continue: true
```

### Tag

This rule type limits the execution of a step to **matching build references**. The below example will run a step if the build ref is `dev/*` or `test/*`:

```yaml
ruleset:
  tag: [ dev/*, test/* ]
```

### Target

This rule type limits the execution of a step to **matching build deployment targets**. The below example will run a step if the build target is `stage` or `production`:

```yaml
ruleset:
  target: [ stage, production ]
```

### Path

This rule type limits the execution of a step to **matching files changed in a repository**. The below example will run a step if file `README.md`, any file of type `*.md` in the root directory or any file in the `test/*` directory has changed:

```yaml
ruleset:
  path: [ README.md, "*.md", "test/*" ]
```

### Comment

This rule type limits the execution of a step to **matching a pull request comment**. This extends the ability to start new builds through interactions within a pull request. The below example will run a step if a "run build" comment is added to the bottom of a pull request.

Note:
* The `comment` event must be enabled for the repo
* The `comment` event must be enabled for any secrets required for the step
* Consider explicitely adding `event` to ruleset for **all** steps as steps with no explicit event(s) will run when the comment matches

```yaml
ruleset:
  comment: [ "run build" ]
```

```yaml
steps:
  - name: echo_always
    image: alpine:latest
    commands:
      - echo "i will always run with 'comment' event"

  - name: echo_never_run_comment
    image: alpine:latest
    commands:
      - echo "i will never run with 'comment' event"
    ruleset:
      event: [ push, pull_request ]

  - name: echo_only_run_comment
    image: alpine:latest
    commands:
      - echo "i will only run with 'comment' event and 'run build' comment"
    ruleset:
      event: [ comment ]
      comment: [ "run build" ]
```

### If

Vela assumes from the above examples that you are implicitly choosing the `if` rules. In other words, the below two examples are interpreted exactly the same to Vela:

```diff
version: "1"

steps:
  - name: test
    image: golang
+   ruleset:
+     branch: master
+     event: push
    commands:
      - go test ./...

  - name: test
    image: golang
+   ruleset:
+     if:
+       branch: master
+       event: push
    commands:
      - go test ./...
```

These rulesets would limit the execution of the step to the build branch is `master` and the build event triggered is a `push` event.

### Unless

If not otherwise provided, Vela assumes evaluation of the logic to **match** the provided rules. However, steps run if the rules **do not match** like below:

```diff
version: "1"

steps:
  - name: test
    image: golang
+   ruleset:
+     unless:
+       branch: master
+       event: push
    commands:
      - go test ./...
```

This ruleset would limit the execution of the step to always run **unless** the build branch is `master` and the build event triggered is `push`.

### Advanced

Vela enables even more advanced conditional triggers by adding the `or` operator. Consider the below example:

```diff
version: "1"

steps:
  - name: test
    image: golang
+   ruleset:
+     event: [ push, pull_request, tag ]
+     tag: release/*
    commands:
      - go test ./...
```

This ruleset would limit the execution of the step to the build event is `push`, `pull_request` or `tag` **AND** the build ref is `release/*`. The problem here is the step would stop executing on `push` and `pull_request` events unless the build ref matched, which is *likely unintended behavior*. To fix it, add the `or` operator:

```diff
version: "1"

steps:
  - name: test
    image: golang
+   ruleset:
+     if:
+       event: [ push, pull_request, tag ]
+       tag: release/*
+     operator: or
    commands:
      - go test ./...
```

This ruleset would limit the execution of the step to the build event is `push`, `pull_request` or `tag` **OR** the build ref is `release/*`.
