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
steps:
  - name: captains-log
    image: target/captains-log:1
    pull: always
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
steps:
  - name: captains-log
    image: target/captains-log:1
    pull: always
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

The plugin accepts the following `parameters` for authentication:

| Parameter      | Environment Variable Configuration |
| -------------- | ---------------------------------- |
| `github_token` | `GITHUB_TOKEN`                     |
| `slack_token`  | `SLACK_URL`                        |
| `slack_url`    | `SLACK_TOKEN`                      |

Users can use [Vela secrets](/docs/tour/secrets/) to substitute these sensitive values at runtime:

```diff
steps:
  - name: captains-log
    image: target/captains-log:1
    pull: always
+   secrets: [ github_token, slack_url ]
    parameters:
      github_owner: target
      github_repo: captains-log
      github_tag_id: "v([0-9]+-release)$"
      enterprise_host: https://git.myteam.com
      jira_team_domain: myteamnamespace
-     github_token: superSecretToken
-     slack_url: https://hooks.slack.com/services/super/secret/url
```

{{% alert color="info" %}}
This example will add the `secrets` to the `captains-log` step as environment variables:

- `GITHUB_TOKEN`=<value>
- `SLACK_URL`=<value>
{{% /alert %}}

## Parameters

For more on configuration options, visit the Captain's Log documentation.

https://target.github.io/captains-log/#/configuration/
