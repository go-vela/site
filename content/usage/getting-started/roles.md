---
title: "Roles"
linkTitle: "Roles"
weight: 2
description: >
  Learn about the authorization roles.
---

{{% alert title="Warning" color="warning" %}}
At this time the only Source Control Provider is GitHub. So this documentation is tailored for those users.
{{% /alert %}}

Vela does not maintain any authentication (AuthN) or authorization (AuthZ) internally, but instead inherits its access from the source (version control) provider. More information on GitHub's access model can be found in their [documentation](https://help.github.com/en/articles/access-permissions-on-github).

Platform Roles:

* Admin

Source Provider Roles:

* Admin
* Write
* Read

### Platform Roles

Platform admins have full control when interacting with the CLI, UI, and API.

### Source Provider Roles:

Admins within the GitHub organization have the option to use GitHub orgs to allow users to have permissions on all repositories in the org, or to use fine-grained access of adding access for users directly to individual repositories.

#### Admin

The **admin** role enables full access to the repository, which grants the following access levels for resources:

| Access | Repo | Build | Step | Service | Log | Secret  |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Write | Y | N | N | N | N | Y |
| Read | Y | Y | Y | Y | Y | Y |

#### Write

The **write** role enables read and write access to the repository, which grants the following access levels for resources:

| Access | Repo | Build | Step | Service | Log | Secret  |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Write | Y | N | N | N | N | N |
| Read | Y | Y | Y | Y | Y | N |

#### Read

The **read** role enables read access to the repository, which grants the following access levels for resources:

| Access | Repo | Build | Step | Service | Log | Secret  |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Write | N | N | N | N | N | N |
| Read | Y | Y | Y | Y | Y | N |
