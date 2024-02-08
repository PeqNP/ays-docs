---
title: "Agent Heartbeat Configuration"
date: 2024-02-08T09:28:02-08:00
draft: false
---

# Agent Heartbeat Configuration

The heartbeat configuration allows you to be alerted if a sensor fails to report within a given period of time.

To configure a heartbeat, please do the following:

```json
{
    "parent": {"property": "path", "value": "com.example.iot"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "child", path: "water-sensor", "monitor_name": "Water Level"},
    "heartbeat": {
        "timeout": 300,
        "level": "critical"
    }
}
```

This will transition the `Water Level` monitor to a `critical` state if the sensor is not heard from within `300` seconds (5 minutes).

The available `level`s are `warning`, `error`, and `critical`.
