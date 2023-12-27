---
title: "@ys 3rd Party Libraries"
date: 2023-12-27T07:53:24-08:00
draft: false
---

# @ys 3rd Party Libraries

The following 3rd party libraries are installed on the main @ys server at `api.bithead.io`.

## `aiohttp` v3.8.5

An asynchronous HTTP client/server for `asyncio` and Python.

[Documentation](https://docs.aiohttp.org/en/stable/)

An instance of the `aiohttp.ClientSession` can be accessed from `session.http`. Below is an example of how to query a website and derive the amount of time it takes to access the resource (this is also the `com.bithead.template.query` template monitor).

### Example Usage

```python
import ays
import time

@ays.param(str, "resource")
@ays.returns("ms")
async def main(session, resource):
    start_time = time.time()
    async with session.http.get(resource) as resp:
        end_time = time.time()
        ms = (end_time - start_time) * 1000
        return ms
```

## `asyncpg` v0.29.0

A database interface designed specifically to work with PostgreSQL and the `asyncio` library.

[Documentation](https://magicstack.github.io/asyncpg/current/)

**NOTE:** Example usage coming soon.

## `beautifulsoup4` v4.11.1

Beautiful Soup is a library that makes it easy to scrape information from web pages.

[Documentation](https://pypi.org/project/beautifulsoup4/)

## `grpcio` v1.59.3

An HTTP/2-based RPC framework.

[Documentation](https://pypi.org/project/grpcio/)

**TODO:** Example usage coming soon.

## `protobuf_to_dict`

Transforms gRPC models into Python dictionaries.

[Documentation](https://github.com/PeqNP/protobuf-to-dict)

## `PyYaml` v6.0

Serialize Python dictionaries to/from YAML.

[Documentation](https://pypi.org/project/PyYAML/)
