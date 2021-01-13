---
title: "Python"
linkTitle: "Python"
description: >
  Learn how the find the documentation for the Python sdk
---

## Overview

Vela Python SDK is a client to perform operations on Vela objects or view content in a new way to integrate into applications. 

For a complete list of APIs and examples, please take a look at the [Python Reference documentation](https://github.com/go-vela/sdk-python#documentation-for-api-endpoints).

## Requirements.

Python 2.7 and 3.4+

## Get build info example

Below is a sample Go program demonstrating how to authenticate and get a build with the Python SDK:

```python
from __future__ import print_function
import time
import vela
from vela.rest import ApiException
from pprint import pprint

# Configure API key authorization: ApiKeyAuth
configuration = vela.Configuration()
configuration.api_key['Authorization'] = 'YOUR_API_KEY'
configuration.api_key_prefix['Authorization'] = 'Bearer'

# Configure API endpoint
configuration.host = 'https://your-vela-server.example.com'

# create an instance of the API class
api_instance = vela.BuildsApi(vela.ApiClient(configuration))

try:
    api_response = api_instance.get_builds(org="go-vela",repo="sdk-python")
    pprint(api_response)
except ApiException as e:
    print("Exception when calling BuildsApi->get_builds: %s\n" % e)
```
