---
title: "Authentication"
linkTitle: "Authentication"
weight: 10
description: >
  Learn how authenticating with the Go SDK works.
---

## Overview

Authentication with the Vela SDK is the responsibility of the client initiating the request.

Each request requires a server address and user token to be provided.

## Sample

Below is a sample Go program demonstrating how to authenticate with the Go SDK:

```go
package main

import (
	"github.com/go-vela/sdk-go/vela"
)

func main() {
	// url is the full URI to the Vela server
	url := "http://localhost:8080"

	// token is the Vela access token given to you from the server
	//
	// TIP: You can get this token by using the /login endpoint
	token := "qwerty123"

	// instantiate a new Vela client
	client, _ := vela.NewClient(url, nil)

	// set the Authentication mechanism for the client
	// to use our access token given from Vela
	client.Authentication.SetTokenAuth(token)
}
```
