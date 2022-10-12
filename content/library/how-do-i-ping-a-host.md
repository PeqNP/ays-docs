---
title: "How Do I Ping a Host"
date: 2022-10-12T07:10:54-07:00
draft: false
---

# How Do I Ping a Host?

This tutorial will show you how to ping a server.

**Please note:** you can associate the Bithead template node `com.bithead.template.ping` to avoid writing this code.

```python
import ays
import time

from ays.api import ping

@ays.param(str, "host")
@ays.returns("ms")
async def main(session, host):
    ms = await ping(host)
    return ms
```

You will notice this sensor imports `ping` from the `ays.api` module. Please refer to the [@ys API Reference]({{< relref "library/ays-api-reference.md" >}}) for more functions.
