---
title: "OpenID Connect"
toc: true
description: >
  Learn how to leverage OpenID Connect for cloud services.
---

### OpenID in Vela

Oftentimes, Vela builds interact with cloud providers to deploy software, update configurations, or more generally use the cloud's services. In order for this process to work securely, users create or retrieve credentials from the cloud provider and duplicate their values into Vela as secrets, which are injected into build steps. As an example, below is a pipeline which uploads a docker image to Artifactory:

```yaml
version: "1"

secrets:
    # password for user Vela-Arti-User
    - name: docker_password
      key: VelaOrg/vela-repo
      type: repo
      engine: native

steps:
    - name: build & publish
      image: target/vela-kaniko:latest
      secrets: [ docker_password ]
      parameters:
        username: Vela-Arti-User
        registry: my-arti-registry.com
        repo: my-arti-registry.com/VelaOrg/vela-repo
        tags:
          - latest
```

The above pipeline will work and be suitable for many cloud-related CI builds. However, there are potential issues with this method. As stricter rotation policies for credentials becomes more common place, developing processes wherein Vela secrets are updated in tandem with these rotations is introducing unneccessary tech debt and is antithetical to continuous integration.

In comes [OpenID Connect](https://openid.net/developers/how-connect-works/).

With OpenID Connect (OIDC), you can configure your pipeline to request a short-lived access token directly from the cloud provider. This requires that the cloud provider supports OIDC processing for Vela ID tokens and properly validates the token using Vela's OpenID configuration and JWKs.

Let's take a look at the same pipeline but using OpenID Connect.

```yaml
version: "1"

steps:
    - name: get credentials
      image: alpine
      id_request: yes
      commands:
        - >
            AUTH_TOKEN=$(curl -H "Authorization: Bearer $VELA_ID_TOKEN_REQUEST_TOKEN"
            "$VELA_ID_TOKEN_REQUEST_URL?audience=artifactory" |
            jq -r '.value')
        - >
            REQ=$(curl -s -X POST -H "Token: $AUTH_TOKEN"
            "https://cloud-service-open-id-validator.com/get-token")
        - echo "${REQ}" | jq -r .username > /vela/secrets/kaniko/username
        - echo "${REQ}" | jq -r .token > /vela/secrets/kaniko/password

    - name: build & publish
      image: target/vela-kaniko:latest
      parameters:
        registry: my-arti-registry.com
        repo: my-arti-registry.com/VelaOrg/vela-repo
        tags:
          - latest
```

In this example, the `get credentials` step is using the Vela environment values of `VELA_ID_TOKEN_REQUEST_TOKEN` and `VELA_ID_TOKEN_REQUEST_URL` to retrieve a short-lived ID token that can be used to authenticate with the cloud service, so long as that service has an OpenID processing layer.

The `id_request` tag being set to _anything_ will result in the injection of the request environment variables. The value of `id_request` becomes a claim in the eventual ID token.

### ID Token Claims

```json
{
   "build_number": 42,
   "build_id": 100,
   "actor": "Octocat",
   "actor_scm_id": "1",
   "repo": "Octocat/vela-testing",
   "token_type": "ID",
   "image": "golang:1.22.4",
   "request": "yes",
   "commands": true,
   "event": "pull_request:opened",
   "ref": "refs/heads/main",
   "sha": "15b17a5751dd2fd04a7b4ca056063dc876984073",
   "iss": "https://vela-server.com/_services/token",
   "sub": "repo:Octocat/vela-testing:ref:refs/heads/main:event:pull_request",
   "aud": [
      "artifactory"
   ],
   "exp": 1717699924,
   "iat": 1717699624
}
```

### Validating an ID Token

There are many resources on validating OpenID tokens. Some of the high level requirements:

- Can the token be validated using the JWKs located at the well-known path of the issuer?
- Do the claims of the ID token match the cloud service expectations?
- Are the claims all members of the `supported_claims` field located at the well-known OpenID configuration?