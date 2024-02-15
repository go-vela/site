---
title: "Working with Templates"
linkTitle: "Working with Templates"
description: >
  Methods of validation and ways to improve template development
---

{{% alert title="Warning" color="warning" %}}
It is highly recommended before reviewing the below content to have a solid grasp on Vela's core concepts that are explored while taking the [Vela Tour](/docs/tour/)).
{{% /alert %}}

When writing a new template getting feedback can be a very painful process. Vela provides a few core methods to get feedback quickly to ensure the template you're writing expands in the pipeline you expect to run. The main methods for seeing expanded pipelines are:

- Pipeline endpoints _(which can be used via UI or CLI)_
- CLI pipeline validation _(`vela validate pipeline`)_


## Pipeline endpoints

This method allows you to evaluate your pipeline that exists within a VCS system. It is most commonly referenced on the build page in the pipeline tab.

Additionally, you can also interact with it the Vela CLI or API if you're trying to create more elaborate workflows.

* [API Docs](/docs/reference/api/pipeline/)

## CLI Pipeline Validation

The CLI workflow that was mentioned above has a variety of methods for local and remote validation. All of them are designed to help you quickly identify areas with your pipeline that need to be improved and should speed up development.

Available Methods:

```sh
# this will continue to validate the file and its nested template(s)
vela validate pipeline

# this will continue to validate via the pipeline endpoints on the server
vela validate pipeline --remote --org MyOrg --repo MyRepo

# this will allow someone to validate a local file with the template expanded
# Note: this method requires the user to provide auth to the template
vela validate pipeline --template

# this will allow someone to override the `source:` and use a local template for testing
vela validate pipeline --template --template-file name:path/to/file
```