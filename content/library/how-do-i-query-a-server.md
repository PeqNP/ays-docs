---
title: "How Do I Query a Server"
date: 2022-10-12T07:21:13-07:00
draft: false
---

# How Do I Query a Server?

This tutorial will show you how to query a HTTP server.

```python
import ays

@ays.param(str, "account_host")
@ays.returns("num_accounts")
async def main(session, account_host):
    async with session.http.get(account_host) as resp:
        data = await resp.json()
        return data["num_accounts"]
```
