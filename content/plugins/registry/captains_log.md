---
title: "Captain's Log"
---

## Overview

The [Captain's Log](https://github.com/target/captains-log) plugin enables the ability to manage release logs through slack in a Vela pipeline.

Source Code: https://github.com/target/captains-log

Registry: https://hub.docker.com/r/target/captains-log

## Usage

Basic Usage

```yaml
image: target/captains-log:1
pull: true
secrets: [GITHUB_TOKEN, SLACK_URL]
parameters:
  github_owner: target
  github_repo: captains-log
  github_tag_id: "v([0-9]+-release)$"
  enterprise_host: https://git.myteam.com
  jira_team_domain: myteamnamespace
```

Utilize "teams" organization:

```yaml
image: target/captains-log:1
pull: true
secrets: [GITHUB_TOKEN, SLACK_URL]
parameters:
  github_owner: target
  github_repo: captains-log
  github_tag_id: "v([0-9]+-release)$"
  enterprise_host: https://git.myteam.com
  jira_team_domain: myteamnamespace
  teams:
    - name: Team1
      color: "#FFDC18"
      emoji: "✨"
      mentions: "<@person1>  <@person2>"
      issueTracking:
        jira:
          projects:
            - TEAM1
            - TEAM1SUBGROUP
    - name: Team2
      color: "#F48642"
      emoji: "🔥"
      mentions: "<@person3>"
      issueTracking:
        jira:
          projects:
            - TEAM2
```

## Secrets

{{% alert color="warning" %}}
Users should refrain from configuring sensitive information in their pipeline in plain text.
{{% /alert %}}

Users can use [Vela secrets](/docs/concepts/pipeline/secrets/) to substitute sensitive values at runtime:

```diff
steps:
  - name: copy_artifacts
    image: target/vela-artifactory:v0.1.0
    pull: true
+   secrets: [ github_token, slack_token, slack_url ]
    parameters:
      action: copy
      path: libs-snapshot-local/foo.txt
      target: libs-snapshot-local/bar.txt
      url: http://localhost:8081/artifactory
```

## Parameters

For more on configuration options, visit the Captain's Log documentation.

https://target.github.io/captains-log/#/configuration/
