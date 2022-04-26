---
title: "Usage"
toc: true
weight: 1
description: >
  Frequently Asked Questions about how to use Vela.
---

## Why is my build not displaying?

This behavior can occur for several reasons that may or may not be visually apparent.

The first step to troubleshooting this issue requires viewing the webhook deliveries for the repository.

This can be accomplished by using one of the following methods:

* **UI** - Navigate to the `https://vela.example.com/<org>/<repo>/hooks` page for the repository
* **CLI** - Run [the `vela get hooks --org <org> --repo <repo>` command for the repository](/docs/reference/cli/hook/get/)

After finding the information for the webhook, please use the list below which includes details on how to resolve the issue.

### Missing Webhook Signature

![Missing Signature](missing_signature.png)

This behavior indicates the signature, used to verify authenticity of the webhook, for the repository has been removed.

To resolve the issue, the repository will need to be repaired which will recreate the webhook with a valid signature.

This can be accomplished by using one of the following methods:

* **UI** - Click the `Repair` button on the `https://vela.example.com/<org>/<repo>/settings` page for the repository
* **CLI** - Run [the `vela repair repo --org <org> --repo <repo>` command for the repository](/docs/reference/cli/repo/repair/)

{{% alert title="Tip:" color="primary" %}}
An access level of `admin` is required in order to repair a repository.
{{% /alert %}}

### Payload Signature Check Failed

![Payload Signature Check Failed](payload_signature_check_failed.png)

This behavior indicates the signature, used to verify authenticity of the webhook, for the repository has been corrupted.

To resolve the issue, the repository will need to be repaired which will recreate the webhook with a valid signature.

This can be accomplished by using one of the following methods:

* **UI** - Click the `Repair` button on the `https://vela.example.com/<org>/<repo>/settings` page for the repository
* **CLI** - Run [the `vela repair repo --org <org> --repo <repo>` command for the repository](/docs/reference/cli/repo/repair/)

{{% alert title="Tip:" color="primary" %}}
An access level of `admin` is required in order to repair a repository.
{{% /alert %}}

### Repo Exceeded Build Limit

![Repo Exceeded Build Limit](repo_exceeded_build_limit.png)

This behavior indicates the number of `pending` or `running` builds for the repository exceeded the concurrent build limit.

To resolve the issue, find a build with a `pending` or `running` status and cancel it (or wait for it to complete).

This can be accomplished by using one of the following methods:

* **UI** - Click the `Cancel Build` button on the `https://vela.example.com/<org>/<repo>/<build>` page for the repository
* **CLI** - Run [the `vela cancel build --org <org> --repo <repo> --build <build>` command for the repository](/docs/reference/cli/build/cancel/)

{{% alert title="Tip:" color="primary" %}}
An alternative solution is to increase the build limit for the repository.

This can be accomplished by using one of the following methods:

* **UI** - Update the `Build Limit` field on the `https://vela.example.com/<org>/<repo>/settings` page for the repository
* **CLI** - Run [the `vela update repo --org <org> --repo <repo> --build.limit <limit>` command for the repository](/docs/reference/cli/repo/update/)
{{% /alert %}}

### Unable To Unmarshal YAML

![Unable To Unmarshal YAML](unable_to_unmarshal_yaml.png)

This behavior indicates the pipeline can't be compiled because it includes invalid syntax.

To resolve the issue, identify the incorrect syntax in the pipeline and update it with proper value(s).

This can be accomplished by using the [`vela validate pipeline` CLI command](/docs/reference/cli/pipeline/validate/) in the directory where the pipeline is located.

### Your Account Was Suspended

![Your Account Was Suspended](your_account_was_suspended.png)

This behavior indicates the user who originally enabled the repository had their account suspended in the SCM.

To resolve the issue, the repository owner will need to be changed to an unsuspended user in the SCM.

This can be accomplished by using one of the following methods:

* **UI** - Click the `Chown` button on the `https://vela.example.com/<org>/<repo>/settings` page for the repository
* **CLI** - Run [the `vela chown repo --org <org> --repo <repo>` command for the repository](/docs/reference/cli/repo/chown/)

{{% alert title="Tip:" color="primary" %}}
An access level of `admin` is required in order to change ownership of a repository.
{{% /alert %}}

## Why is my build not running?

This behavior can occur for several reasons that may or may not be visually apparent.

The first step to troubleshooting this issue requires viewing the build object for the repository.

This can be accomplished by using one of the following methods:

* **UI** - Navigate to the `https://vela.example.com/<org>/<repo>` page for the repository
* **CLI** - Run [the `vela get builds --org <org> --repo <repo>` command for the repository](/docs/reference/cli/build/get/)

After finding the information for the build, please use the list below which includes details on how to resolve the issue.

### Build Is Pending

![Build Is Pending](build_is_pending.png)

This behavior indicates the number of `running` builds for the system is greater than the number of [workers](/docs/administration/worker/) available.

Unfortunately, the only way to resolve the issue is to wait until a worker becomes available to run your build.

### Context Deadline Exceeded

![Context Deadline Exceeded](context_deadline_exceeded.png)

This behavior indicates the amount of time the build was `running` exceeded the timeout for the repository.

To resolve the issue, optimize the pipeline to improve the performance and decrease the runtime for builds.

This can be accomplished by using one of the following methods:

* Update the pipeline [to use rulesets](/docs/tour/rulesets/) which will limit the number of [steps](/docs/tour/step/) ran in the build
* Update the pipeline [to use stages](/docs/tour/stages/) which will enable running [steps](/docs/tour/step/) concurrently

{{% alert title="Tip:" color="primary" %}}
An alternative solution is to increase the build timeout for the repository.

This can be accomplished by using one of the following methods:

* **UI** - Update the `Build Timeout` field on the `https://vela.example.com/<org>/<repo>/settings` page for the repository
* **CLI** - Run [the `vela update repo --org <org> --repo <repo> --timeout <timeout>` command for the repository](/docs/reference/cli/repo/update/)
{{% /alert %}}

### Invalid Reference Format

![Invalid Reference Format](invalid_reference_format.png)

This behavior indicates [the `image` key](/docs/tour/image/) provided for a step in the pipeline is invalid.

To resolve the issue, identify the step with the incorrect `image` and update it with a proper value.

This can be accomplished by using the [`docker pull` CLI command](https://docs.docker.com/engine/reference/commandline/pull/) with the value for the `image` as the first argument.

### Invalid Secret Path

![Invalid Secret Path](invalid_secret_path.png)

This behavior indicates [the `key` property](/docs/reference/yaml/secrets/#the-key-tag) provided for a secret in the pipeline is invalid.

To resolve the issue, explicitly define the secret depending on the type as outlined in the [secret usage docs](/docs/usage/secrets/) with all of the expected fields.

If you are using a secret that only defines `name` as the property and are receiving this error, you will need add the missing properties as this way of referencing a secret was deprecated in an older version of Vela.

For example:
```yaml
secrets:
  - name: foo
```

would need to be changed to:

```diff
secrets:
  - name: foo
+   key: <org>/<repo>/foo
+   engine: native
+   type: repo
```

{{% alert title="Tip:" color="primary" %}}
Make sure to replace `<org>` and `<repo>` for the `key` property with the appropriate values from your source code provider.

If you're using GitHub and using the secret for a pipeline at `https://github.com/octocat/hello`, your `org` would be `octocat` and `repo` would be `hello`.
{{% /alert %}} 