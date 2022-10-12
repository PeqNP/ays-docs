---
title: "How Do I Configure a Measurement Sensor"
date: 2022-10-11T19:24:46-07:00
draft: false
---

# How Do I Configure a Measurment Sensor?

A script sensor allows you to run a script (such as Python) at a given interval (every 15 seconds, 1 minute, etc.).

Every sensor must configure at least one threshold. The threshold defines the severity of the issue and min and max range that a queried data point must be inside of, lest the measurement be considered "unhealthy."

# The Composition of a Sensor Script

This script is an example that shows you all of the available inputs and return types.

```python
# Import the `ays` library. You are not restricted as to which libraries
# you can import. To avoid making changes to the database, do not import
# anything from `ays_lib`.
import ays

# These are all of the supported parameters that can be provided to a
# sensor function.
@ays.param(str, "http_path")
@ays.param(int, "status")
@ays.param(bool, "enabled")
@ays.param(float, "percent")
# A sensor function may return a single optional `int` OR it can return
# an array of optional `int`s.
@ays.returns("num_requests")
# Syntax to return an array of optional `int`s.
# @ays.returns(["num_requests", "ms"])
async def main(session, http_path, status, enabled, percent):
    # Query a remote service that returns JSON
    async with session.http.get(http_path) as resp:
        data = await resp.json()
        # Return the data value. Again, this must be an optional `int`
        return data["num_requests"]
```

**Please note:** You *must* return `null` (`None` in the Python context) if the data collection operation fails. `null` data points will emit an alert.

# Template Measurements

Please refer to [What is a Template Node?]({{< relref "library/what-is-a-template-node.md" >}}) first, in order to understand the function of templates.

If you find that you are writing the same sensor code for more than one measurment, consider writing a template measurement. A template measurement is like a re-usable function. For example, if your team has several services that can be measured in the same way, you may consider creating a template measurement.

## Common Sensor Operations

- [How do I ping a host?]({{< relref "library/how-do-i-ping-a-host.md" >}})
- [How do I query a HTTP server?]({{< relref "library/how-do-i-query-a-server.md" >}})
