---
title: "Agent Reports Status Value"
date: 2024-02-08T09:26:51-08:00
draft: false
---

# Report a Status

Reporting a status is useful for systems that don't report values but _can_ report the state of a machine.

If you use a tool like NewRelic you can use their alerting platform to define the state of a system. Typically you would write a NRQL query, associate a health state (error, critical, etc.), and then send a message to Slack. In many cases you already have this configuration setup! To report to **@ys**, simply have a catch-all webhook that reports NRQL alerts to **@ys**. Each alert type will be treated as a separate monitor. This gives you granular information about the state of your system.

To send a status, please do the following:

```json
{
    "parent": {"property": "path", "value": "com.example.mobile.ios"},
    "org_secret": "my_org_secret",
    "relationship": {"type": "parent", "monitor_name": "Max. Error Breached"},
    "status": {
        "message": "Max. error breached",
        "state": "critical"
    }
}
```

This will associate a monitor, with name `Max. Error Breached`, to the parent node `com.example.mobile.ios`. The state of the monitor will transition to `critical`. The possible states are `healthy`, `warning`, `error`, and `critical`.

**NOTE:** If you select the sample, within the monitor graph, the sample will display the `message`.

## Curing a Status

There are two ways to cure an unhealthy status:

- The 3rd party system sends a "healthy" signal. This is done by setting the value of `state` to `healthy`. The `monitor_name` value must match for this to work.
- Directly within **@ys**. Navigate to the respective agent monitor and tap the `Clear` button.
