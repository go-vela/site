---
title: "Token Manager"
linkTitle: "Token Manager"
weight: 6
description: >
  This section contains information on the token manager component for the Vela server.
---

This component is responsible for generating and validating JWT tokens shared between the Vela server, workers, and users based off the configuration provided.

The token manager is designed to ensure secure interactions with the server and protect build resources.


## Configuration

The following options are used to configure the component:

| Name                             | Description                                                                                                                     | Required | Default   | Environment Variables                         |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | -------- | --------- | --------------------------------------------- |
| `vela-server-private-key`        | private key used for signing and validating all JWT tokens                                                                      | `true`   | `N/A`     | `VELA_SERVER_PRIVATE_KEY`                                                   |
| `user-access-token-duration`     | maximum duration of time a Vela access token for a user is valid on the server                                                  | `true`   | `15m`     | `VELA_USER_ACCESS_TOKEN_DURATION`<br>`USER_ACCESS_TOKEN_DURATION`           |
| `user-refresh-token-duration`    | maximum duration of time a Vela refresh token for a user is valid on the server                                                 | `true`   | `8h`      | `VELA_USER_ACCESS_TOKEN_DURATION`<br>`USER_ACCESS_TOKEN_DURATION`           |
| `build-token-buffer-duration`    | maximum duration of time a Vela build token for a build extends beyond the repo build limit to maintain validity on the server  | `true`   | `5m`      | `VELA_BUILD_TOKEN_BUFFER_DURATION`<br>`BUILD_TOKEN_BUFFER_DURATION`         |
| `worker-auth-token-duration`     | maximum duration of time an auth token for a worker is valid on the server                                                      | `false`*   | `20m`     | `VELA_WORKER_AUTH_TOKEN_DURATION`<br>`WORKER_AUTH_TOKEN_DURATION`           |
| `worker-register-token-duration` | maximum duration of time a registration token for a worker is valid on the server                                               | `false`*   | `1m`      | `VELA_WORKER_REGISTER_TOKEN_DURATION`<br>`WORKER_REGISTER_TOKEN_DURATION`   |



{{% alert title="Notes:" color="primary" %}}
\* `worker-auth-token-duration` and `worker-register-token-duration` are required if you intend to register workers.

For more information on these configuration options, please see the [server reference](/docs/installation/server/reference/).
{{% /alert %}}
